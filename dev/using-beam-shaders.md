# Using Beam Shaders

In this tutorial we will describe how to use Beam Shaders on DAPPNET

{% hint style="info" %}
Why DAPPNET?&#x20;

Beam has three public networks: Dappnet, Testnet and Mainnet

Dappnet has fake mining and produces a block every 15 seconds. It is recommended for writing and testing DApps and was created specifically for this purpose

Testnet has real mining and is mostly used as final testing ground before Mainnet releases

Mainnet is live Beam network with real assets
{% endhint %}

### Downloading DAPPNET wallet

To get started, download the latest version of Beam Dappnet Wallet from [Beam Website](https://beam.mw/downloads/dappnet)

Install the wallet using default settings. This will run a local node that we will use to run our Shaders. Create a new wallet, and save the seed for future use.&#x20;

{% hint style="info" %}
We will keep the Desktop Wallet running during our work, since we are going to use the integrated node to run our shaders
{% endhint %}

### Get some Beam from the Faucet

Since every Beam transaction is accompanied by a fee paid in BEAM coins, we will need to get some positive balance in our wallet in order to be able to run our Shaders.

Open the DApp Store by clicking the icon on the left vertical menu bar and find a Faucet Application.&#x20;

<figure><img src=".gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

Open the Faucet and click on 'Get your first BEAM' button. Then click 'Confirm' and wait for the transaction to complete.

<figure><img src=".gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

### Setting up CLI wallet

In this part of the tutorial we will invoke shaders using a CLI wallet. You can download the walelt from the [same location](https://beam.mw/downloads/dappnet) as the Desktop wallet before that.

Create an empty folder (in this tutorial we are using Windows, but you can use Mac or Linux instead) and copy the contents of the CLI wallet archive. You should see two files: the CLI wallet executable and the config file for the wallet.&#x20;

### Copy wallet.db from Desktop Wallet

wallet.db holds all information related to the wallet data. We will use the same wallet.db from the Desktop Wallet that we have installed in the previous step.&#x20;

{% hint style="warning" %}
It is not recommended to do this in real wallets, but for the development purposes it is ok
{% endhint %}

The wallet.db file is located in %LOCALAPPDATA%\Beam Wallet folder. Copy it to the same folder with the CLI wallet executable

{% hint style="info" %}
On other operating systems, check documentation for wallet.db location or check the Troubleshooting section in Desktop Wallet Settings screen


{% endhint %}

<figure><img src=".gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

Configure CLI wallet settings

Before we start running shaders, let's configure the CLI wallet settings to make our command lines shorter and simpler. We are going to connect our CLI wallet to the built in node running. Open the beam-wallet.cfg file in your favorite text editor and set the following parameters:

`log_level=debug`

`pass=<your wallet password>`

`node_addr=127.0.0.1:10005`

`wallet_path=wallet.db`

As as result your configuration file should look something like this:

<pre><code><strong>################################################################################
</strong># General options:
################################################################################

# log level [info|debug|verbose]
log_level=debug

# file log level [info|debug|verbose]
# file_log_level=debug

# old logs cleanup period (days)
# log_cleanup_days=5

################################################################################
# Wallet options:
################################################################################

# password for the wallet
pass=123

# phrase to generate secret key according to BIP-39.
# seed_phrase=

# address of node
node_addr=127.0.0.1:10005

# path to wallet file
wallet_path=wallet.db

# command to execute [new_addr|send|receive|listen|init|info|export_miner_key|export_owner_key|generate_phrase]
# command=listen


</code></pre>

Now we are ready to run Shaders, all that's left is to choose which shaders to run ))

### Getting the Application Shader file&#x20;

The simplest way to find a contract on Dappnet is to open the [Dappnet Blockchain Explorer](https://dappnet.explorer.beam.mw/) and scroll down to the list of blocks. Then click on the Contracts tab

<figure><img src=".gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

We will use the first one in the list, a test contract called Vault. It is very simple and we will use it in all our examples throughout the tutorial

{% hint style="info" %}
At the time of writing list of contracts is only added on Dappnet. Also, most of the deployed contracts do not have readable description. We will add this part in the upcoming releases.
{% endhint %}

In order to run commands again this Contract Shader, we will need to download the matching Application Shader from Beam Repository. In the next parts of this tutorial we will see how to implement and build these Shaders but for now we will use a precompiled one that is committed alongside the source code [here](https://github.com/BeamMW/beam/tree/master/bvm/Shaders/vault).

Download the app.wasm file and copy it to the same folder as the CLI walle executable. If you are planning to test several applications, it is convenient to create a folder for each one. So you can create a folder called vault and put the app.wasm file under it.

### Running Shader commands

Open as command line interface and change directory to the location of the CLI wallet executable.&#x20;

First thing we will do is print the API of the contract by running the following command:

`beam-wallet-dappnet.exe shader --shader_app_file vault\app.wasm`

Note that we only provide one parameter (--shader\_app\_file) since we assume all other parameters are set in the configuration file. We also provide a path to the application shader assuming it is located in the 'vault' folder.

The output of this command will look something like this (debug logs are on in this example)

<figure><img src=".gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

Let's copy the Shader output part into the text editor and format it to a standard JSON form. The end results will look like this:

```json
 {
     "roles":
     {
         "manager":
         {
             "create":
             {},
             "destroy":
             {
                 "cid": "ContractID"
             },
             "view":
             {},
             "view_logs":
             {
                 "cid": "ContractID"
             },
             "view_accounts":
             {
                 "cid": "ContractID"
             },
             "view_account":
             {
                 "cid": "ContractID",
                 "pubKey": "PubKey"
             }
         },
         "my_account":
         {
             "view":
             {
                 "cid": "ContractID"
             },
             "get_key":
             {
                 "cid": "ContractID"
             },
             "get_proof":
             {
                 "cid": "ContractID",
                 "aid": "AssetID"
             },
             "deposit":
             {
                 "cid": "ContractID",
                 "pkForeign": "PubKey",
                 "bCoSigner": "uint32_t",
                 "amount": "Amount",
                 "aid": "AssetID"
             },
             "withdraw":
             {
                 "cid": "ContractID",
                 "pkForeign": "PubKey",
                 "bCoSigner": "uint32_t",
                 "amount": "Amount",
                 "aid": "AssetID",
                 "amountCoSigner": "Amount"
             }
         }
     }
 }
```

What you see here is the API of the Vault contract as it is presented by the Application Shader we have used. The API actions are separated into roles, in this case 'manager' and 'my\_account'. Roles are only used as semantic grouping.

Let's use the 'view\_accounts' method to list all accounts in the Vault

Since we are going to be working with a specific Contract Shader we will need to use the contract id that we have copied from the blockchain explorer: \
`d9c5d1782b2d2b6f733486be480bb0d8bcf34d5fdc63bbac996ed76af541cc14`

Let's run the following command:

`beam-wallet-dappnet.exe shader --shader_app_file vault\app.wasm --shader_args=cid=d9c5d1782b2d2b6f733486be480bb0d8bcf34d5fdc63bbac996ed76af541cc14,role=manager,action=view_accounts`

The output will show us something similar to this:

<figure><img src=".gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

In this case there are currently no accounts in the contract. Let's create one using a 'deposit' method. Let's start with depositing 1 BEAM. To do that we will run the following command:

`beam-wallet-dappnet.exe shader --shader_app_file vault\app.wasm --shader_args="cid=d9c5d1782b2d2b6f733486be480bb0d8bcf34d5fdc63bbac996ed76af541cc14,role=my_account,action=deposit,amount=100000000"`

Note that amount is set in Groth, which is 1^10-8 of BEAM.&#x20;

This action will take some time to complete since the transaction is created and sent to the network. The result will be similar to this:

<figure><img src=".gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

The important part is the one here which explains what happened

<figure><img src=".gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

Let's run the 'accounts' command again and see if anything changed?

<figure><img src=".gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

Indeed, now we see that there is a new account identified by a public key and having a balance of 1 Beam. As an exercise you are invited tp do the same, and also get your BEAM back. You can try to get BEAM from someone elses account (hint: you can't).



In the next part of the tutorial we will see how to code this contract and deploy it on chain.&#x20;