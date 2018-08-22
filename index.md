## Noded Bitcoin Meetup

Here are the resources from the meetup. For any clarification please hit up the group on [Slack](https://join.slack.com/t/beijingbitcoinmeetup/shared_invite/enQtNDE5MjUzNjkwNjQ0LTkxOTFjNmMyOTg2ZjI3ZTZlZGExYTFiN2M3ODcyNGVjNGY0YmJkNWRhZGM2OTU1M2FiNDI1OTlkYWE2Yjg2NjQ)

**Warning** This tutoial is for information purposes only. In order to be able to get a functioning system up within a reasonable timeframe I have ignored several factors to consider when setting up your own node such as:

- Using a hosted provider is less ideal than running off your own hardware
- Running as a root is not recommended
- Firewall rules have not been considered
- Using a Ubuntu package is less trusted than building from source yourself

Most importantly **I do not know what I'm doing** - following these steps should be considered REKLESS

But hey ho, let's go:

## SSH

1. Open up a Terminal window and create a public/private key pairing for the purpose of accessing your remote server:`ssh-keygen -t rsa`
2. Save the key in the default location `/Users/[YOURNAME]/.ssh/` using the filename beijing (i.e. `/Users/satoshinakamoto/.ssh/beijing`
3. Enter and reenter a passphrase to secure your private key

## Digital Ocean

4. Go to https://www.digitalocean.com (hopefully you have already signed up in advance)
5. Click Create > Droplets
6. In the options select Ubuntu, 4GB/2CPUs
7. Under Add Blcok Storage select Add Volume and select 250GB
8. Under Datacentre Region select San Francisco 2
9. Under Add your SSH keys, click New SSH key
11. Access the folder on your laptop as per Step2 (e.g. `/Users/satoshinakamoto/.ssh/beijing`), and open the beijing.pub file using a text editor (I like [Atom](https://atom.io)), copy the whole contents and paste into the box on digitalocean
12. Under Choose a hostname input `beijing`
13. Wait for the droplet to be created
14. Once created, copy the IP address next to the Droplet name

## Access your new server

15. `ssh root@[IP] -i /Users/[username]/.ssh/beijing` (see Step 2 for the filepath)
16. Type `yes`
17. Enter passphrase
18. You are now in root@beijing :)

## Time to Bitcoin

19. sudo apt-add-repository ppa:bitcoin/bitcoin (enter to confirm)
20. sudo apt-get update
21. sudo apt-get install bitcoind
22. mkdir ~/.bitcoin
23. nano ~/.bitcoin/bitcoin.conf
24. Copy and paste the `bicoin.conf` text into the terminal window
25. Ctrl+X to exit Y to save
26. You are ready to go! `bitcoind -daemon` and you will be on your way!
27. `bitcoin-cli getblockcount` will show you how many blocks you have downloaded
28. Before you have your first block you can check `bitcoin-cli getblockchaininfo` to show more detailed informations - so long as the number of `headers` is rising then you are on your way!

## Switcharoo

You are now syncing your own bitcoin node. Congratulations! This will take over 24hrs...so I have followed the above steps for y'all in advance for you to use for the rest of today's activities.

## Post-Sync

29. Access your server by: `ssh root@[IP] -i /Users/satoshinakamoto/.ssh/beijing`?????????????????

## Lightning

30. Install the prerequisites: `sudo apt-get install -y \ autoconf automake build-essential git libtool libgmp-dev \ libsqlite3-dev python python3 net-tools zlib1g-dev`
31. Get the software: `git clone https://github.com/ElementsProject/lightning.git`
32. `cd lightning`
33. `./configure`
34. `make`
35. `lightningd/lightningd --network=bitcoin --bitcoin-datadir=/mnt/volume-sfo2-02 --bitcoin-rpcuser=foo --bitcoin-rpcpassword=bar --log-level=debug` ??????????????

## Getting Ready For Btcpayserver

36. We need to install a bunch of Microsoft packages - `wget -q https://packages.microsoft.com/config/ubuntu/16.04/packages-microsoft-prod.deb`
37. `sudo dpkg -i packages-microsoft-prod.deb`
38. `sudo apt-get install apt-transport-https`
39. `sudo apt-get update`
40. `sudo apt-get install dotnet-sdk-2.1`

## Now let's get NBXplorer - a blockchain explorer which Btcpayserver references

41. `git clone https://github.com/dgarage/NBXplorer.git`
42. `cd NBXplorer`
43. `./build.sh`

## Easy - now for btcpayserver

44. `cd` to get back to the root directory
45. `git clone https://github.com/btcpayserver/btcpayserver.git`
46. `cd btcpayserver`
47. `./build.sh`

## OK - Everything installed now...almost there...

48. `cd` to get back to the root directory
49. `cd NBXplorer`
50. `/run.sh --btcrpcuser=foo --btcrpcpassword=bar`
51. `cd` to get back to the root directory
52. `cd .btcpayserver/Main`
53. `nano settings.config`
54. Make sure some text is displayed - if not check you got the previosu steps right. Find the line beginning `# bind`. Delete the `#` and add your Droplet IP
55. `cd`
56. `cd btcpayserver`
57. `./run.sh`

## I wonder if it worked...

58. Open an exlporer and navigate to http://[YOURIP]:23000
59. Pray
60. All being well you'll be on the Btcpayserver homepage - this is your very own payment processing system!
61. Click Register and enter your email address and password (note the first sign up will be given admin access, all subsequent sign-ups will not)
62. Check your Terminal window running btcpayserver - hopefully you should se your registration creating an event
63. Clcik Stores > Create a new store and name it 'test'
64. In the store settings go to Derivation Scheme and click Modify
65. Input your publickey (recommned zpub!)
66. Make sure to check the addressses match one of your receiving addresses before confirming!
67. 
### Need more help

Use [Slack](https://join.slack.com/t/beijingbitcoinmeetup/shared_invite/enQtNDE5MjUzNjkwNjQ0LTkxOTFjNmMyOTg2ZjI3ZTZlZGExYTFiN2M3ODcyNGVjNGY0YmJkNWRhZGM2OTU1M2FiNDI1OTlkYWE2Yjg2NjQ) and hopefully we can share our experiences in getting this working! 

