# The Use Cases of Online Advertising

Discussion Paper for the  
W3C Advertising Business Group

Contibutors:
* Wendell Baker <[wbaker@verizonmedia.com](mailto:wbaker@verizonmedia.com)\>  
* Michael Kleber <[kleber@google.com](mailto:kleber@google.com)\>

Draft, updated 2019-04-16

This document describes event sequences supporting modern online advertising. Many details are elided. There is a significant amount of tutorial literature available which can be used to fill in the details and omissions that are necessarily present in this summary document.

## Dramatis Personae

The web advertising ecosystem is a collaboration among many parties.  Common designations like "third-party" can often be ambiguous when a single pageload involves interactions with servers run by many organizations with different roles, needs, and capabilities.  So we begin with a list of types of parties and what roles they play.

* **Publisher:**
  Publishers produce web pages that users visit.  Most of the time, you can think of the publisher as the first party (though aggregation and syndication sites can add a little confusion).
  
  Since we're discussing the web ads ecosystem, the publisher web pages we care about will generally have ads on them.  That means you can think of publishers as creating web pages containing _empty rectangles_ — rectangles which they want to sell to advertisers.  Since publishers sell empty rectangles, they are referred to as the _sell side_ or the _supply side_ of the market.  The empty rectangles themselves are sometimes referred to as _ad slots_, or as _inventory_ when thinking of them as something being sold.
  
  Publishers generally have a lot of control over their content, but the amount of control they have over the advertisements on their pages varies a lot; see "Publisher Ad Platform" below.
  
* **Advertiser:**
  Advertisers want to show some message to people visiting publishers' web sites, and are willing to pay money to publishers to do so.  Their messages are the ads, also called _creatives_, and can include text, images, video, JavaScript, and so on — all the capabilities of a web page.  Creatives  usually fit into a standard-sized rectangle, meant to fill in one of the empty rectangles on a publisher page.
  
  Since advertisers buy rectangle-shaped real estate to put their ads in, they are referred to as the _buy side_ or the _demand side_ of the market.  When a specific ad creative appears on a user's load of a publisher web page, the event is called an _impression_.
  
  The advertiser might pay by the impression, or might only pay if a user actually clicks on the ad.  Many advertisers have some goal beyond the impression or click — they might want the user to sign up for their newsletter, buy something on their web site, etc.  Those later target events are called _conversions_.


## Ad Call with Single Market

![Event Flow Diagram](https://w3c.github.io/web-advertising/UseCasesofOnlineAdvertising/image1.png)

### Steps

1.  UserBrowser calls Publisher Web App (Web Site) asking for content
2.  Content is returned
3.  UserBrowser calls Publisher Content Server to assemble the page
4.  Content is returned
5.  UserBrowser calls the Ad Marketplace “give me an ad”
6.  Creative Code is returned
7.  UserBrowser calls the Creative Payload Server
8.  Creative Payload is returned
9.  UserBrowser calls a Content Delivery Network to recover the payload (images).
10.  Payloads are returned.

### Background Activities

*   Counting jof a Page Delivered occurs at the Publisher Web App (Web Site)
*   Counting of a Sale occurs at the Ad Market
*   Counting of a Page Viewed occurs a the Creative Payload service.

### Other Considerations

*   There may be many marketplaces (Steps 5 & 6) in a cascade or waterfall.
*   There may be many creative payload services (Steps 7 & 8), each providing a different business capability: fraud mitigation, visibility verification, conversion counting, and so forth.
*   The UserBrowser may solicit from multiple marketplaces simultaneously, resolving the winner in the consumer premises equipment.
*   Each marketplace may have a deeper structure with subcalls to other services and other marketplaces with whch they trade.
