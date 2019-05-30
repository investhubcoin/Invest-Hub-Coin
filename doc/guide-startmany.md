#start-many Setup Guide

## Two Options for Setting up your Wallet
There are many ways to setup a wallet to support start-many. This guide will walk through two of them.

1. [Importing an existing wallet (recommended if you are consolidating wallets).](#option1)
2. [Sending 10,000 IHC to new wallet addresses.](#option2)

## <a name="option1"></a>Option 1. Importing an existing wallet

This is the way to go if you are consolidating multiple wallets into one that supports start-many. 

### From your single-instance MasterNode Wallet

Open your QT Wallet and go to console (from the menu select Tools => Debug Console)

Dump the private key from your MasterNode's pulic key.

```
walletpassphrase [your_wallet_passphrase] 600
dumpprivkey [mn_public_key]
```

Copy the resulting priviate key. You'll use it in the next step.

### From your multi-instance MasterNode Wallet

Open your QT Wallet and go to console (from the menu select Tools => Debug Console)

Import the private key from the step above.

```
walletpassphrase [your_wallet_passphrase] 600
importprivkey [single_instance_private_key]
```

The wallet will re-scan and you will see your available balance increase by the amount that was in the imported wallet.

[Skip Option 2. and go to Create masternode.conf file](#masternodeconf)

## <a name="option2"></a>Option 2. Starting with a new wallet

[If you used Option 1 above, then you can skip down to Create masternode.conf file.](#masternodeconf)

### Create New Wallet Addresses

1. Open the QT Wallet.
2. Click the Receive tab.
3. Fill in the form to request a payment.
    * Label: mn01
    * Amount: 1000 (optional)
    * Click *Request payment*
5. Click the *Copy Address* button

Create a new wallet address for each MasterNode.

Close your QT Wallet.

### Send 10,000 IHC to New Addresses

Just like setting up a standard MN. Send exactly 10,000 IHC to each new address created above.

### Create New Masternode Private Keys

Open your QT Wallet and go to console (from the menu select Tools => Debug Console)

Issue the following:

```masternode genkey```

*Note: A masternode private key will need to be created for each MasterNode you run. You should not use the same masternode private key for multiple MasterNodes.*

Close your QT Wallet.

## <a name="masternodeconf"></a>Create masternode.conf file

Remember... this is local. Make sure your QT is not running.

Create the masternode.conf file in the same directory as your wallet.dat.

Copy the masternode private key and correspondig collateral output transaction that holds the 1K IHC.

The masternode private key may be an existing key from [Option 1](#option1), or a newly generated key from [Option 2](#option2). 

*Please note, the masternode priviate key is not the same as a wallet private key. Never put your wallet private key in the masternode.conf file. That is equivalent to putting your 10,000 IHC on the remote server and defeats the purpose of a hot/cold setup.*

### Get the collateral output

Open your QT Wallet and go to console (from the menu select Tools => Debug Console)

Issue the following:

```masternode outputs```

Make note of the hash (which is your collaterla_output) and index.

### Enter your MasterNode details into your masternode.conf file
[From the IHC github repo](https://github.com/ihcfund/ihc-core/blob/master/doc/masternode_conf.md)

The new masternode.conf format consists of a space seperated text file. Each line consisting of an alias, IP address followed by port, masternode private key, collateral output transaction id and collateral output index, donation address and donation percentage (the latter two are optional and should be in format "address:percentage").

```
alias ipaddress:port masternode_private_key collateral_output collateral_output_index donationin_address:donation_percentage
```



Example:

```
mn01 127.0.0.1:34100 7i5S8We5d7E2WRVTyizNX1ytjEf5iR5ChbyT4dp6399G2ZW6zjF f96bb531c80617c1214c248aad6d0ac1ad6b1e6081627864b164be7048dc5dc3 0
mn02 127.0.0.2:34100 7iVhkVB2UZbrTXtyPnQgPCU6carsyuKGaFy2WczwmxoLCuJZnmP 288dc8426ed92a9446ee4d6cc95edfa0e9ffa1ac7661f1fb1089f75b3c01a38c 0 PKFhiRbVYkhPgTNYJQKE9KuwTDbSGaXXWA:25
```

## What about the ihc.conf file?

If you are using a masternode.conf file you no longer need the ihc.conf file. The exception is if you need custom settings (thanks oblox). 

## Update ihc.conf on server

If you generated a new masternode private key, you will need to update the remote ihc.conf files.

Shut down the daemon and then edit the file.

```sudo nano .ihc/ihc.conf```

### Edit the masternodeprivkey
If you generated a new masternode private key, you will need to update the masternodeprivkey value in your remote ihc.conf file.

## Start your MasterNodes

### Remote

If your remote server is not running, start your remote daemon as you normally would. 

I usually confirm that remote is on the correct block by issuing:

```ihcd getinfo```

And compare with the official explorer at http://ihc.fund

### Local

Finally... time to start from local.

#### Open up your QT Wallet

From the menu select Tools => Debug Console

If you want to review your masternode.conf setting before starting the MasterNodes, issue the following in the Debug Console:

```masternode list-conf```

Give it the eye-ball test. If satisfied, you can start your nodes one of two ways.

1. masternode start-alias [alias_from_masternode.conf]. Example ```masternode start-alias mn01```
2. masternode start-many