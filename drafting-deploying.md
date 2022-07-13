# Drafting and Deploying Khronus Client Contract

## Drafting your Client Contract:

* You need to install the Khronus Utils

    - If you are using [Brownie Eth](https://eth-brownie.readthedocs.io/en/stable/) or other not JS based frameworks, it is recommended that you install the utilities directly from the [github repository](https://github.com/Khronus-Project/Khronus_utils)  
    - In JS based frameworks or Remix you can utilize NPM style imports (see below), this will import the utilities directly from NPM [https://www.npmjs.com/package/@khronus/khronus-utils](https://www.npmjs.com/package/@khronus/khronus-utils) without needing to install the utilities directly.

* Importing the client base:

    - If using the direct imports (In remix or JS based framework), you can just add the following line.

```
\\Direct imports
import "@khronus/khronus-utils@0.0.2/contracts/KhronusClientBase.sol";
```
   
   - If you imported all the utilities as a package, you'll need to do this in brownie, you refer directly to the documentation of the specific framework you are using.

```
\\Import after local installation of the utilities
import "khronus-project/khronus_utils@0.0.3/contracts/KhronusClientBase.sol";
```
    
    - Many frameworks allow to configure how to refer to imported files. In brownie for example you could modify your brownie-config.yaml as follows:

```
dependencies:
    - khronus-project/khronus_utils@0.0.3
compiler:
    solc:
        remappings:
        - "@khronus/khronus-utils@0.0.3=khronus-project/khronus_utils@0.0.3"
source networks:
    default: local
```

## Client Contract Functions:

The client contract base contains the following functions:

```
function clientRequestKhronTab(uint256 _timestamp, uint256 _iterations, uint256 _step) internal returns (bytes32){
    require(KhronusTimeCog.isValidTimestamp(_timestamp), "the timestamp is not valid");
    uint256 _processedTimestamp = _processTimeStamp(_timestamp);
    return KhronusCoordinator.requestKhronTab(_processedTimestamp, _iterations, _step);
}

function khronProcessAlert(bytes32 _requestID) internal virtual returns (bool) {
}

function khronResponse(bytes32 _requestID) external returns (bool){
    require (msg.sender == khronusCoordinator);
    khronProcessAlert(_requestID);
    return true;
}
```

### Request KhronTab Function:

- the Request Khron Tab Function takes three parameters, the timestamp when the alert should trigger, the number of iterations of the alert, and the step of the alert. 

    - The timestamp (_timestamp) should be a timestamp in the [unix standard](https://en.wikipedia.org/wiki/Unix_time) that happens in the future.
    - The number of iterations is how many alerts should be triggered, currently Khronus supports only 1 iterations alerts.
    - The step or timeframe between each iteration, currently at beta this should be set to 0.
    - This function only registers the alert in the network, it doesn't define what happens upon expiration.
    - The function returns the RequestId as a bytes32 hexadecimal value.

- Example: The following function creates a Khronus powered escrow that expires in the selected timestamp.

```
function openEscrow(address _beneficiary, uint256 _expiryTimestamp, address _agent) external payable returns (bytes32){
    address _depositor = msg.sender;
    uint256 _deposit = msg.value; 
    bytes32 _escrowID = keccak256(abi.encodePacked(_depositor, nonce));
    escrowRegistry[_escrowID].balance = _deposit;
    escrowRegistry[_escrowID].expiryTimestamp = _expiryTimestamp;
    escrowRegistry[_escrowID].depositor = _depositor;  
    escrowRegistry[_escrowID].beneficiary = _beneficiary;
    escrowRegistry[_escrowID].agent = _agent;
    escrowRegistry[_escrowID].condition = false;
    escrowRegistry[_escrowID].status = EscrowStatus.Open;
    bytes32 _requestID = clientRequestKhronTab(_expiryTimestamp, 1, 0);
    tabRegistry[_requestID] = _escrowID;
    nonce += 1;
    emit EscrowCreated(_depositor, _escrowID, _expiryTimestamp, _deposit);
    return _escrowID;
}
```

### The Khron Process Alert Function

- This function is originally empty in the contract base, you need to override it with the logic you want to implement upon the expiration of the alerts. This logic of this function is up to you, but the function is internal it can only be triggered by the khronResponse external function, which only can be called by the Khronus Protocol.

- Example: The following function is the counterpart to the create alert function above, this function actually expires the escrow and transfers the escrow funds according to the escrow rules. 

```
function khronProcessAlert(bytes32 _requestID) override internal returns (bool){
    bytes32 _escrowID = tabRegistry[_requestID];
    if (escrowRegistry[_escrowID].condition){
        payable(escrowRegistry[_escrowID].beneficiary).transfer(escrowRegistry[_escrowID].balance);
        escrowRegistry[_escrowID].balance = 0;
        escrowRegistry[_escrowID].status = EscrowStatus.Expired;
    }
    else{
        payable(escrowRegistry[_escrowID].depositor).transfer(escrowRegistry[_escrowID].balance);
        escrowRegistry[_escrowID].balance = 0;
        escrowRegistry[_escrowID].status = EscrowStatus.Expired;
    }
    emit EscrowExpired(_escrowID, block.timestamp, escrowRegistry[_escrowID].condition);
    return true;
}
```

# The Khron Response Function:
- This function is not open to be modified.