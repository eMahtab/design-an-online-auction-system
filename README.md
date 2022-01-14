# Design an online auction system

## System requirements :
1. An auction is initiated by a seller and consists of a single product. The seller can edit an auction till it is in draft state. The seller can start an auction and can define a start and end date. The auction is started once it is moved to publish state. It starts from 0$ and buyers can keep bidding (current_bid + a predefined increment) until it expires.

2. The seller can define a reserve price. Its presence is visible, but the actual amount is not. If defined and the final bid is less than the reserve price, the auction will fail with a separate status.

3. Buyers should be allowed to see any auction details including the product details which is being sold in that auction.

4. Buyers should also be allowed to subscribe to an auction i.e. they should be notified of any change in the auction. While the auction is live, buyers can bid for the product. Buyers who bid in the auction automatically become the subscriber of that auction. The seller is always a subscriber of the auction. Whenever the auction state changes, subscribers are notified.

### Rough class diagram 
![Class Diagram](auction-system.png?raw=true)

# References :
https://www.youtube.com/watch?v=5fdKUzfMk4E
https://github.com/MayV/OnlineAuctionSystem
