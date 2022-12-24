# NFT-DAPP MARKETPLACE
 
# Introduction

The advent of blockchain technology, a decentralized ledger on which digital assets can be created and exchanged peer-to-peer, has shifted the conventional understanding of ownership. These digital assets are often referred to as tokens, and we can use them as a medium of exchange like a currency, a representation of a physical or digital item, or even an identity attribute like a driver’s license.
Ethereum, the second-largest blockchain by market capital and the first blockchain to launch smart contracts, is a blockchain network that offers a flexible platform on which we can build decentralized applications using the native Solidity scripting language and Ethereum Virtual Machine. These decentralized applications are composed of smart contracts or programmable logic that allows transactions of tokens such as issuing new tokens, transferring tokens between accounts based on different conditions, or exchanging tokens. The programmability enabled by smart contracts lets developers create many forms of digital assets or tokens, such as USD Coin (USDC), a popular fungible cryptocurrency pegged to the value of the US dollar. 
Recently, a renaissance of digital art, collectibles, and digital assets like certificates of valuation or authority has emerged from adopting another form of token: non-fungible tokens (NFTs).

# System Architecture

The front-end of the NFT application is deployed to Amazon S3 and can be accessed via Amazon CloudFront. Users can sign up and log in to this application. Once a user creates an Asset, it is stored in an S3 bucket, and Amazon CloudFront will distribute this asset to the NFT space. We implemented the business logic and connected the front-end client application to the blockchain network using Amazon API Gateway and AWS Lambda, to provide a highly secure and scalable solution. The Lambda function works with Amazon Managed Blockchain to provide seamless access to the Ethereum network for sending and monitoring transactions. We have integrated this architecture with purpose-built databases to store data outside of the blockchain network. 

![alt text](https://github.com/takhilabhinav/simple-nft-marketplace-aws/blob/main/imgs/simple-nft-marketplace.png)

# Product Features

1.Create a NFT Listing
2.Transfer Asset to another user
3.Buy Asset 
4.Sell Asset
5.Transfer ETH

# AWS Services Employed

1. Amazon Simple Storage Service (Amazon S3 Bucket) for Front-end website hosting
2. Amazon Simple Storage Service for assets
3. API Gateway
4. AWS Cognito for authentication
5. Lambda
6. Dynamo DB
7. CloudFront
8. Amazon Managed BlockChain
9. Ethereum Network


# API Endpoints

1. /getUser/ - GET request to assist in getting user related data for setting up the home page.

2. /assets/createasset - POST request used for assisting the user to create a new NFT Asset. 

3. /assets/getasset - GET request used for assisting user to fetch NFT Asset details.

4. /list/createitem - POST request used for assisting users to list an asset on the marketplace.

5. /list/getitem - GET request used for getting user’s asset details listed on the marketplace.

6. /list/purchase - POST request used for assisting users to buy an NFT Asset.

7. /list/unlist - POST request used for assisting users to unlist an asset from the marketplace.

# Workflow/User Journey
 							
User Signup/Login: We have used AWS Cognito Service for completing this step. Amazon Cognito is a simple user identity and data synchronization service that helps us securely manage and synchronize app data for users across their mobile devices. We can create unique identities for the users through a number of public login providers (Amazon, Facebook, and Google) and also support unauthenticated guests.

Create NFT: User can register a new asset by choosing ‘Create Asset’, which shows a form that collects some basic information such as asset name, description about the asset, and an initial price in Ether for the asset. This information is passed to the API Gateway endpoint /createitem, which generates a unique ID for the asset and passes this ID to a smart contract. The smart contract function mints a new NFT and associates the asset’s unique ID with the NFT token ID. This REST API function further saves the asset ID, NFT token ID, and the data sent to it by the UI application into Amazon Dynamo DB table for querying purposes.

Show NFT: After an asset is registered and an NFT has been minted, the NFT is available for buying and selling in the marketplace. The token id of the registered asset is passed to the API gateway endpoint /getitem, which fetches the details about the specific asset. The specific owner can transfer the asset to another user too. To do that, /transferitem API endpoint is called which takes as input the receiver private key and transfers the asset. Two things need to happen when an NFT is transferred from a buyer to a seller. First, the smart contract updates the owner address of the NFT and then the Ether balance needs to be adjusted from the buyer to the seller account. 
In order for a marketplace to adjust a buyer and seller’s Ether balance, it needs to create a balance transfer transaction between the buyer and seller for the purchased NFT amount. To complete this transfer, this transaction must be signed with the buyer’s private key.

# Future Plans:

1. Emphasis on improving the user experience. This could involve features such as a more intuitive and user-friendly interface, better search functionality, and more robust support for different types of NFTs.

2. More focus on increasing the liquidity and accessibility of NFTs. This could involve the integration of payment gateways or other financial services that make it easier for users to buy and sell NFTs. It could also involve the development of tools and features that make it easier for users to discover and evaluate NFTs.

3. Focus on building and strengthening their communities. This could involve the creation of forums, social media groups, or other spaces where users can interact with each other and discuss NFTs and other topics related to the app.

# Outputs 
[!alt text](https://github.com/takhilabhinav/simple-nft-marketplace-aws/blob/main/imgs/Screen%20Shot%202022-12-23%20at%209.54.31%20PM.png)
[!alt text](https://github.com/takhilabhinav/simple-nft-marketplace-aws/blob/main/imgs/Screen%20Shot%202022-12-23%20at%209.54.48%20PM.png)
[!alt text](https://github.com/takhilabhinav/simple-nft-marketplace-aws/blob/main/imgs/Screen%20Shot%202022-12-23%20at%209.55.04%20PM.png)
