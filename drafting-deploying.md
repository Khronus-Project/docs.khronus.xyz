# Drafting and Deploying Khronus Client Contract

# Drafting your Client Contract:
* You need to install the Khronus Utils
    * You can install the utilities directly from the [github repository](https://github.com/Khronus-Project/Khronus_utils) if you are using [Brownie Eth](https://eth-brownie.readthedocs.io/en/stable/) or other not JS based frameworks. 
    * In JS based frameworks or Remix you can utilize NPM style imports such as: ```import @khronus/khronus-utils...``` this will import directly from NPM [https://www.npmjs.com/package/@khronus/khronus-utils](https://www.npmjs.com/package/@khronus/khronus-utils) without needing to install the utilities directly.
* Importing the client base:
    * If using the direct imports (In remix or JS based framework), you can just add the following line.
    ```
    \\Direct imports
    import "@khronus/khronus-utils@0.0.2/contracts/KhronusClientBase.sol";
    ```
    * If you imported all the utilities as a package, you'll need to do this in brownie, you refer directly to the documentation of the specific framework you are using.
    ```
    \\Import after local installation of the utilities
    import "khronus-project/khronus_utils@0.0.3/contracts/KhronusClientBase.sol";
    ```
    * Many frameworks allow to configure how to refer to imported files. In brownie for example you could modify your brownie-config.yaml as follows:
    ```
    dependencies:
        - khronus-project/khronus_utils@0.0.3
    compiler:
        solc:
            remappings:
            - "@khronus/khronus-utils@0.0.3=khronus-project/khronus_utils@0.0.3"
    source networks:
        default: local

