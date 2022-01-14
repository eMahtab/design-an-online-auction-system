# Design an online auction system

## System requirements :
1. An auction is initiated by a seller and consists of a single product. The seller can edit an auction till it is in draft state. The seller can start an auction and can define a start and end date. The auction is started once it is moved to publish state. It starts from 0$ and buyers can keep bidding (current_bid + a predefined increment) until it expires.

2. The seller can define a reserve price. Its presence is visible, but the actual amount is not. If defined and the final bid is less than the reserve price, the auction will fail with a separate status.

3. Buyers should be allowed to see any auction details including the product details which is being sold in that auction.

4. Buyers should also be allowed to subscribe to an auction i.e. they should be notified of any change in the auction. While the auction is live, buyers can bid for the product. Buyers who bid in the auction automatically become the subscriber of that auction. The seller is always a subscriber of the auction. Whenever the auction state changes, subscribers are notified.

## Features :

1. Register a seller/buyer.
2. Seller can create a new auction which will always go in DRAFT state.
3. Seller can add product details in an auction which is in DRAFT state & can also mention the base price for the product.
4. Seller can publish an auction given all necessary details have been added. Seller can schedule an auction while publishing the auction.
5. Seller can view his auction details.
6. Buyers can view any auction details.
7. Buyers can subscribe/unsubscribe to an auction.
8. Buyers can bid in an auction.
9. When the auction state changes, a notification is sent to all the subscribers.
10. Sellers/Buyers can view their latest ‘x’ notifications.

### Rough class diagram 
![Class Diagram](auction-system.png?raw=true)

## User 
```java
import com.sun.istack.internal.NotNull;

import java.util.LinkedList;
import java.util.List;

public class User extends Observer {
	private String userId;
	private String username;
	private String emailId;
	private String phoneNo;
	private List<Notification> notifications; //Always insert latest data at the head of the list.
	// TODO - private List<BankAccountDetails> bankAccountDetils;
	// TODO - private List<Address> addresses;

	public User(@NotNull String userId, @NotNull String username, @NotNull String emailId, @NotNull String phoneNo) {
		this.userId = userId;
		this.username = username;
		this.emailId = emailId;
		this.phoneNo = phoneNo;
		this.notifications = new LinkedList<>();
	}

	public String getUserId() {
		return userId;
	}

	public void setUserId(String userId) {
		this.userId = userId;
	}
	
	public String getUsername() {
		return username;
	}

	public void setUsername(String username) {
		this.username = username;
	}

	public String getEmailId() {
		return emailId;
	}

	public void setEmailId(String emailId) {
		this.emailId = emailId;
	}

	public String getPhoneNo() {
		return phoneNo;
	}

	public void setPhoneNo(String phoneNo) {
		this.phoneNo = phoneNo;
	}

	public List<Notification> getNotifications() {
		return notifications;
	}

	@Override
	public boolean equals(Object obj) {
		if(obj==null) {
			return false;
		}
		if(obj instanceof User) {
			return this.username.equals(((User) obj).getUsername());
		}
		return false;
	}
}
```

## Auction 
```java
import com.sun.istack.internal.NotNull;

import java.util.Date;
import java.util.List;

public class Auction extends Publisher{
	private String auctionId;
	private String sellerId;
	private List<AuctionProduct> products;	//Singleton List
	private AuctionState auctionState;
	private Date startDate;
	private Date endDate;
	
	public Auction(@NotNull String auctionId) {
		super();
		this.auctionId = auctionId;
		this.auctionState = AuctionState.DRAFTED;
	}

	public String getAuctionId() {
		return auctionId;
	}

	public void setAuctionId(String auctionId) {
		this.auctionId = auctionId;
	}

	public String getSellerId() {
		return sellerId;
	}

	public void setSellerId(String sellerId) {
		this.sellerId = sellerId;
	}

	public AuctionState getAuctionState() {
		return auctionState;
	}

	public void setAuctionState(AuctionState auctionState) {
		this.auctionState = auctionState;
	}

	public List<AuctionProduct> getProducts() {
		return products;
	}

	public void setProducts(List<AuctionProduct> products) {
		this.products = products;
	}

	public Date getStartDate() {
		return startDate;
	}

	public void setStartDate(Date startDate) {
		this.startDate = startDate;
	}

	public Date getEndDate() {
		return endDate;
	}

	public void setEndDate(Date endDate) {
		this.endDate = endDate;
	}

	@Override
	public boolean equals(Object obj) {
		if(obj==null) {
			return false;
		}
		if(obj instanceof Auction) {
			return this.getAuctionId().equals(((Auction) obj).getAuctionId());
		}
		return false;
	}
}
```

# References :
https://www.youtube.com/watch?v=5fdKUzfMk4E

https://github.com/MayV/OnlineAuctionSystem
