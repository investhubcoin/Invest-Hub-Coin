# IHC
Shell script to install a [IHC Masternode](https://ihc.fund/) on a Linux server running Ubuntu 16.04. Use it on your own risk.
***

## Installation
```
wget -q https://raw.githubusercontent.com/ihcfund/ihc-core/master/ihc_install.sh

bash ihc_install.sh
```
***

## Desktop Wallet Setup 

After the MN is up and running, you need to configure the desktop wallet accordingly. Here are the steps:  
1. Open the IHC(IHC) Desktop Wallet.  
2. Go to RECEIVE and create a New Address: **MN1**  
3. Send **1000** IHC to **MN1**. You need to send all 1000 coins in one single transaction.
4. Wait for 15 confirmations.  
5. Go to **Help -> "Debug Window - Console"**  
6. Type the following command: **masternode outputs**  
7. Go to  **Tools -> "Open Masternode Configuration File"**
8. Add the following entry:
```
Alias Address Privkey TxHash TxIndex
```
* Alias: **MN1**
* Address: **VPS_IP:PORT**
* Privkey: **Masternode Private Key**
* TxHash: **First value from Step 6**
* TxIndex:  **Second value from Step 6**
9. Save and close the file.
10. Go to **Masternode Tab**. If you tab is not shown, please enable it from: **Settings - Options - Wallet - Show Masternodes Tab**
11. Click **Update status** to see your node. If it is not shown, close the wallet and start it again. Make sure the wallet is un
12. Select your MN and click **Start Alias** to start it.
13. Alternatively, open **Debug Console** and type:
```
startmasternode "alias" "0" "my_mn"
``` 
14. Login to your VPS and check your masternode status by running the following command:
```
ihc-cli masternode status
```
***

## Usage:
```
ihc-cli masternode status  
ihc-cli getinfo
```
Also, if you want to check/start/stop **IHC**, run one of the following commands as **root**:
```
systemctl status IHC #To check if IHC service is running  
systemctl start IHC #To start IHC service  
systemctl stop IHC #To stop IHC service  
systemctl is-enabled IHC #To check if IHC service is enabled on boot  
```  
***
Credit to @Zoldur for writing the original install script.

https://github.com/zoldur
