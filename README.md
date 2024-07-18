# Allora Basic Node V2 Migration.

Use this Command
```bash
  cd $HOME
```
You will Move to your HOME directory.

```bash
  docker-compose ls
```
Copy the you node files Path as shown Highlight in image.(in my case its ```/root/basic-coin-prediction-node ``` )
![image](https://github.com/user-attachments/assets/ebbe003d-f2f4-4add-93c4-dc1a70f68433)

```bash
  cd /root/basic-coin-prediction-node && ls
```
sample output  
![image](https://github.com/user-attachments/assets/4d169021-f41c-4c0d-8017-5cdc4b094349)


Run Following Command to down you worker
```bash
  docker-compose down
```
sample output  
![image](https://github.com/user-attachments/assets/1209eaa1-223e-4985-be1a-dfd2293b5dbd)  

Run followwing command one-by-one
```bash
  docker stop $(docker ps -aq) 2>/dev/null
```
```bash
  docker rm $(docker ps -aq) 2>/dev/null
```
```bash
  docker rmi -f $(docker images -aq) 2>/dev/null
```
Note : Check ```docker ps``` if node container running, output will be none.

Now, Copy the Command and Run it.
```bash
  sed -i 's|--allora-node-rpc-address=https://allora-rpc.edgenet.allora.network/|--allora-node-rpc-address=https://allora-rpc.testnet-1.testnet.allora.network/|' docker-compose.yml
```
Run, following Command to live your node to network.
```bash
  docker-compose up -d
```
sample output  
![image](https://github.com/user-attachments/assets/40053b5f-1793-46ca-b0bf-88da4ceb7f9a)

# Voila! You have Successfully upgrade to V2 Testnet.  

Check Node Status by Running Following Command. 
```bash
  $(curl --silent --location 'http://localhost:6000/api/v1/functions/execute' \
--header 'Content-Type: application/json' \
--data '{
    "function_id": "bafybeigpiwl3o73zvvl6dxdqu7zqcub5mhg65jiky2xqb4rdhfmikswzqm",
    "method": "allora-inference-function.wasm",
    "parameters": null,
    "topic": "1",
    "config": {
        "env_vars": [
            {
                "name": "BLS_REQUEST_PATH",
                "value": "/api"
            },
            {
                "name": "ALLORA_ARG_PARAMS",
                "value": "ETH"
            },
        ],
        "number_of_nodes": -1,
        "timeout": 2
    }
}')

```

check ```CODE : 200``` and ```infernce value```it should change over the time.



