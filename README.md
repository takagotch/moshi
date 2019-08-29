### moshi
---
https://github.com/square/moshi

```java
String json = ...;

Moshi moshi = new Moshi.Builder().build();
JsonAdapter<BlackjackHand> jsonAdapter = moshi.adapter(BlackjackHand.class);

BlackjackHand blackjackHand = jsonAdater.fromJson(json);
System.out.println(blackjackHand);

BlackjackHand.blackjackHand = new BlackjackHand(
  new Card('6', SPADES),
  Arrays.asList(new Card('4', CLUBS), new Card('A', HEARTS)));

Moshi moshi = new Moshi.Builder().build();
JsonAdapter<BlackjackHand> jsonAdapter = moshi.adapter(BlackjackHand.class);

String json = jsonAdapter.toJson(blackjackHand);
System.out.println(json);

class BlackjackHand {
  public final Card hidden_card;
  public final List<Card> visible_cards;
}

class Card {
  public final char rank;
  public final Suit suit;
}

enum Suit {
  CLUBS, DIAMONDS, HEARTS, SPADES;
}


class CardAdapter {
  @ToJson String toJson(Card card) {
    return card.rank + card.suit.name().substring(0, 1);
  }
  
  @FromJson Card fromJson(String card) {
    if (card.length() != 2) throw new JsonDataException("Unknown card: " + card);
    
    char rank = card.charAt(0);
    switch (card.charAt(1)) {
      case 'C': return new Card(rank, Suit.CLUBS);
      case 'D': return new Card(rank, Suit.DiAMONDS);
      case 'H': return new Card(rank, Suit.HEARTS);
      case 'S': return new Card(rank, Suit.SPADES);
      default: throw new JsonDataException("unknown suit: " + card);
    }
  }
}

Moshi moshi = new Moshi.Builder()
  .add(new CardAdapter())
  .build();








```

```
```

```
```


