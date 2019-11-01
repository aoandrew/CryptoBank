# CryptoBank
Crypto Bank

Banks are built on trust.  The trusted middleman of money transfer.  It is the center of personal finance and corporate finance.

Banks provide more than a "place to put your money."  They provide loans, escrow services, checks against amounts, transfer of money, cutting checks to individuals or businesses, activity reports, and can change who controls funds.  They also can make loans using deposit assets for a variety of types of loans including car loans, home loans, business loans, etc.

Technology makes banks efficient but of course adds a layer of risk.  Banks have layers of technical security mediated of course by their own secured records.  As such, APIs against bank funds corporately and personally are not aways very open.  Security-first is a good approach to preserving your money.

Crypto bank is an open-source project that aims to create a API first bank that fullfulls all functions of a bank from the "hodling" of your money, to the transfer of funds, to the escrow and loan services.  Also, secure financial records that have financial impact - like "who invested" in this entity, how much money has passed through the entity, how much is owed to and from the organization.

It will be API-first making it very easy for online companies to use the service in addition to end-customers using the bank. 

- Ideally the bank would have a mobile and web presence not unlike current offerings.  
- Records would be kept on public widely distributed decentralized blockchains with low concentration ideally.
- Protocols / blockchains would be interchangable so newer technology could be incorporated by the bank, but also so that future users of the code of the bank could simply swap out protocols / blockchains without having to fork and make significant changes to the code.  (ie. pre-baking flexibility to maintain cohesion of developer community to create strength to crypto bank code base, allow crypto bank operator flexibility, and in-the end allow users choice.  The added benefit of course would be the interoperability of the crypto banking network - escrow, loans, paybacks, verications, payments - so much of the value depends on the network effects (interoperability) of the financial network. 

Entities would be treated and controlled in a similar fashion to objects:


Escrow:
```
public class RiverEscrow : Escrow, IPublicTranscribeable
{
  //OWNERSHIP
  public List<EntityObserverers> EObserverers {get;set;} //DECLARE THOSE THAT CAN OBSERVE EVENTS AND PROPERTIES

  public EscrowCreator ECreator {get; set;}  //CREATOR OF ESCROW 
  public List<EntityController> EControllers {get;set;}  //THOSE THAT CAN SEND MONEY
  public List<EntityReceivers> EReceivers {get;set;}  //REGISTER RECEIVERS
  
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

Governance:
Common sense Multi-sig schemes or Threshhold signature schemes make sense for security but also for the transition banking organizations to blockchain mediated ones.

This allows for governments / regulators / management of the bank to make changes to the bank, approve transactions if necessary, or reverse transactions if necessary.

The governance structure will mirror the rights of current legal structures (in contrast to fully "trustless" systems.)
