Getting started with the wallet
===============================

Tedchain Server exposes a `public HTTP API <http-api>`, which can be called by any program capable of making HTTP calls.

To wrap all those operations in a user-friendly user interface, we also provide a client: the Tedchain Wallet.

The Tedchain Wallet is an open source web based interface, available at `wallet.tedchain.network <https://wallet.tedchain.network>`_.

Connecting to a server
----------------------

The wallet is a client side application running in the browser, and capable of connecting to any Tedchain endpoint. It can connect to multiple endpoints at the same time, and pull information and submit transactions to multiple instances of Tedchain, however the first time you use it, you need to connect to at least one endpoint.

![alt tag](https://i.imgur.com/9uwWQaJ.png)

The first page invites you to connect to an endpoint. Click the link to use the test endpoint provided by Tedlab, then click "Check endpoint". The wallet will then try to connect to the Tedchain instance and retrieve the instance information.

![alt tag](https://i.imgur.com/DaokjGr.png)

Confirm to connect to this endpoint.

Note: The Tedchain wallet will memorize the endpoint you are connecting to, so you will only have to perform this step once.

Logging in
----------

The wallet will now ask you to provide a mnemonic seed used to derive your private key and address.

![alt tag](https://i.imgur.com/98Uqm4l.png)

Click "Create a new wallet" if you want to generate a new mnemonic, and reuse one you have already generated. Click "Sign in" to confirm. After the key has been derived from your seed, you should see your home screen:

![alt tag](https://i.imgur.com/8UDorw4.png)

You are now able to receive payments on the Tedchain instance by giving your account path to the payer (``/p2pkh/n2yYKCsho8gDrr53SUtzgtKCBypD3JMUxo/`` in the example above).

Issue an asset
--------------

The test endpoint provided by TedLab has third party asset issuance enabled, so we can now issue an asset.

To do this, click the "Assets" tab.

![alt tag](https://i.imgur.com/WHA1yAY.png)

Select the endpoint and the first slot, and click "Confirm".

![alt tag](https://i.imgur.com/pES1ORw.png)
   
Click "Issue Asset" and type an amount to issue (10000 for example). Press "Issue".

You should then see a confirmation of the transaction.

![alt tag](https://i.imgur.com/X30lEcX.png)
   
Your account should have been updated with the newly issued asset.

![alt tag](https://i.imgur.com/MzwoOEV.png)

Tip: You can use the "Edit Asset Definition" box in the asset issuance page to define `metadata <asset-metadata>` about your asset, such as a name and icon.

Send a payment
--------------

Now that we have funds, we can send them.

Click the newly issued asset to be taken to the "Send" page.

![alt tag](https://i.imgur.com/7gjOmqN.png)
   
Type a valid destination, such as ``/p2pkh/mfiCwNxuFYMtb5ytCacgzDAineD2GNCnYo/``, and a valid amount.

Press "Send" to confirm. If the transaction went through successfully, you should see the transaction confirmation screen.

![alt tag](https://i.imgur.com/X30lEcX.png)

Admin tools
-----------

The wallet also has admin tools built-in.

Ledger tree view
----------

The ledger tree view displays a visual representation of the `account hierarchy <account-hierarchy>`. The details of the record selected on the left will be showed on the right hand side.

![alt tag](https://i.imgur.com/XQa7sz6.png)

Alias editor
----------

The alias editor lets you configure `aliases <aliases>` for specific paths. After an alias has been set, it is possible to send funds to the alias directly using the ``@`` prefix. The wallet will automatically resolve the alias.

Note: In the default permission layout, aliases can only be modified by an administrator.