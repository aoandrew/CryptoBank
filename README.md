# CryptoBank
Crypto Bank

Banks are built on trust.  The trusted middleman of money transfer.  It is the center of personal finance and corporate finance.

Banks provide more than a "place to put your money."  They provide loans, escrow services, checks against amounts, transfer of money, cutting checks to individuals or businesses, activity reports, and can change who controls funds.  They also can make loans using deposit assets for a variety of types of loans including car loans, home loans, business loans, etc.

Technology makes banks efficient but of course adds a layer of risk.  Banks have layers of technical security mediated of course by their own secured records.  As such, APIs against bank funds corporately and personally are not always very open.  Security-first is a good approach to preserving your money.

Crypto bank is an open-source project that aims to create a API first bank that fulfills all functions of a bank from the "hodling" of your money, to the transfer of funds, to the escrow and loan services.  Also, secure financial records that have financial impact - like "who invested" in this entity, how much money has passed through the entity, how much is owed to and from the organization.

It will be API-first making it very easy for online companies to use the service in addition to end-customers using the bank. 

- Ideally the bank would have a mobile and web presence not unlike current offerings.  
- Records would be kept on public widely distributed decentralized blockchains with low concentration ideally.
- Protocols / blockchains would be interchangeable so newer technology could be incorporated by the bank, but also so that future users of the code of the bank could simply swap out protocols / blockchains without having to fork and make significant changes to the code.  (ie. pre-baking flexibility to maintain cohesion of developer community to create strength to crypto bank code base, allow crypto bank operator flexibility, and in-the end allow users choice.  The added benefit of course would be the interoperability of the crypto banking network - escrow, loans, paybacks, verifications, payments - so much of the value depends on the network effects (interoperability) of the financial network. 

Entities would be treated and controlled in a similar fashion to objects:


Escrow:
```
public class RiverEscrow : Escrow, IPublicTranscribeable
{
  //OWNERSHIP
  public List<EntityObserverers> EObserverers {get;set;} //DECLARE THOSE THAT CAN OBSERVE EVENTS AND PROPERTIES

  public EscrowCreator ECreator {get; set;}  //CREATOR OF ESCROW 
  public List<EntityController> EControllers {get;set;}  //THOSE THAT CAN SEND MONEY
  public List<EntityReceivers> EReceivers {get;set;}  //REGISTER RECEIVERS
  
  //FUNDS
  public double TotalFunds {get;set;}
  
  //TRANSACTIONS + PROPERTY CHANGES
  public List<Transactions> ETransactions {get;set;} //KEEP TRACK OF TRANSACTIONS - RUNNING IMMUTABLE RECORD (BLOCKCHAIN)
  public List<PropertyChanges> EPropertyChanges {get;set;} //KEEP TRACK OF CHANGES TO PROPERTIES - RUNNING IMMUTABLE RECORD
  public ApprovableList<Transactions> EIncomingPayments {get;set;} //INCOMING TRANSACTIONS - AFTER ACCEPTANCE, IT WILL BE REMOVED - RUNNING IMMUTABLE RECORD (BLOCKCHAIN)

  public RiverEscrow()
  {}
  
  private SendTo(Entity sentToEntity, AmountToSend amountToSend)
  {
    //MAKE SURE THAT sentToEntity IS PART OF THE RECEIVER LIST
    //CHECK IF SUFFICIENT FUNDS, THEN SUBTRACT SEND AMOUNT 
  };
  
  private AcceptTransaction(string incomingTransactionsId, ApprovableList<Transactions> approvableList)
  {
    //ACCEPT INCOMING FUNDS VIA TRANSACTION ID FROM THE EIncomingPayments list
    //ITEMS SHOULD BE REMOVED FROM APPROVABLELIST
  };  
}


```


Since this Escrow subclasses IPublicTranscribable, it can be used via the following:

```
var reviewEscrow = ShowAllRecords(RiverEscrow, Format.FormattedView); //Format.TemporalView, Format.ReverseTemporalView, Format.SummaryView

```

Accounts should have a Checking and Savings account to mirror current banking situations.

Additionally each account type should have an unlimited number of Wallets each with it's own permissions.

```

enum AccountType
{
    Checking,
    Savings
}

public class Account : IPayable
{
  public AccountType AccountType {get;set;}
  public int Amount {set;set;}
  
  //Return amount in account including all wallets
  public int SumIncludingAllWallets(Guid id)
  {
    ...
    return amount;
  }

  //Return amount in account including all wallets
  public int SumExcludingAllWallets(Guid id)
  {
    ...
    return amount;
  }


}

public class Wallet : IPayable
{
  public Guid Id {get;set;}
  
  public bool IsReceivingOnly {get;set;}
  
  public bool SendFromWalletToWallet(Guid idToSendFrom, Guid idToSendTo)
  {
  
    return success;
  }
}
```
Accounts would have a more restricted permission set.

Wallets id numbers could be shared -- so a vendor could pay to or be paid from a specific wallet only.  Permissions and the amount that is allowed to flow through could be more clearly set on the wallet level to prevent fraud.  Wallets could be emptied into the account on a specified schedule (time or amount).

Also wallets can easily be created or destroyed for increased privacy.

Governance:
Common sense Multi-Sig schemes or Threshold Signature Schemes make sense for security but also for the transition banking organizations to blockchain mediated ones.

This allows for governments / regulators / management of the bank to make changes to the bank, approve transactions if necessary, or reverse transactions if necessary.

The governance structure will mirror the rights of current legal structures (in contrast to fully "trustless" systems.)
