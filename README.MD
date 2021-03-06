![Logo](https://raw.githubusercontent.com/raulbojalil/bitso-dotnet/master/logo.png "Logo")

# Bitso .NET Client API

This is a .NET Client API for the mexican cryptocurrency exchange Bitso. https://bitso.com/api_info.

## Supported APIs

* Public API
* Private API
* Account Creation API

## Installation

Run the following command in the Package Manager Console:
```
Install-Package Bitso.Net
```
See the package at [Nuget.org](https://www.nuget.org/packages/Bitso.Net).

## Usage

Create a new instance of the Bitso Class using the following parameters:
* API Key and Secret Key. You can get these at https://bitso.com/api_setup. These values are not needed for the Public API.
* Is Production. A boolean value that indicates whether or not to target the Production environment. Default value = false.

```C# 
var bitsoClient = new Bitso("[YOUR API KEY]", "[YOUR SECRET KEY]", true);

//Get Available Books (Public API)
var books = bitsoClient.PublicAPI.GetAvailableBooks();

//Get the user's Account Status (Private API)
var accountStatus = bitsoClient.PrivateAPI.GetAccountStatus();
```

## Public API

#### Available Books

Returns a list of existing exchange order books and their respective order placement limits.

```C# 
BookInfo[] books = bitsoClient.PublicAPI.GetAvailableBooks();
```

#### Ticker

Returns trading information from the specified book.

```C# 
Ticker ticker = bitsoClient.PublicAPI.GetTicker("btc_mxn");
```

#### Order Book

Returns a list of all open orders in the specified book. If the aggregate parameter is set to true, orders will be aggregated by price, and the response will only include the top 50 orders for each side of the book. If the aggregate parameter is set to false, the response will include the full order book.

```C# 
OrderBook orderBook = bitsoClient.PublicAPI.GetOrderBook("btc_mxn", aggregate: true);
```

#### Trades

Returns a list of recent trades from the specified book.

```C# 
Trade[] trades = bitsoClient.PublicAPI.GetTrades(
    book: "btc_mxn", //MXN/BTC Book
    limit: 10,  //Objects to return
    sort: "asc" //Ordering direction 
);
```

## Private API

TODO

## Exception Handling

Wrap your code around a try-catch block and catch the BitsoException type. The BitsoException class contains an ErrorCode property with the error code returned from the Bitso API. For a list of error codes please go to: https://bitso.com/developers#error-codes.

```C# 
try
{
    var response = bitsoClient.PrivateAPI.XXXXX();
}
catch(BitsoException ex)
{
    Console.WriteLine(ex.ErrorCode);
}
```










