// DigimonDeckBuilder.jsx
import React, { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Input } from "@/components/ui/input";
import { Button } from "@/components/ui/button";

const mockCards = [
  {
    id: 1,
    name: "Agumon",
    level: 3,
    color: "Red",
    type: "Dinosaur",
    img: "https://www.digimoncard.dev/images/cards/BT1-010.jpg",
  },
  {
    id: 2,
    name: "Gabumon",
    level: 3,
    color: "Blue",
    type: "Reptile",
    img: "https://www.digimoncard.dev/images/cards/BT1-020.jpg",
  },
];

export default function DigimonDeckBuilder() {
  const [search, setSearch] = useState("");
  const [deck, setDeck] = useState([]);

  const filteredCards = mockCards.filter((card) =>
    card.name.toLowerCase().includes(search.toLowerCase())
  );

  const addToDeck = (card) => {
    if (deck.length < 50) setDeck([...deck, card]);
  };

  const removeFromDeck = (index) => {
    const newDeck = [...deck];
    newDeck.splice(index, 1);
    setDeck(newDeck);
  };

  return (
    <div className="p-4 grid grid-cols-1 md:grid-cols-2 gap-6">
      <div>
        <h2 className="text-xl font-bold mb-2">Recherche de cartes</h2>
        <Input
          placeholder="Nom de la carte..."
          value={search}
          onChange={(e) => setSearch(e.target.value)}
        />
        <div className="grid grid-cols-2 gap-4 mt-4">
          {filteredCards.map((card) => (
            <Card key={card.id} className="cursor-pointer" onClick={() => addToDeck(card)}>
              <CardContent className="p-2">
                <img src={card.img} alt={card.name} className="rounded-xl" />
                <p className="text-sm text-center mt-1">{card.name}</p>
              </CardContent>
            </Card>
          ))}
        </div>
      </div>
      <div>
        <h2 className="text-xl font-bold mb-2">Mon deck ({deck.length}/50)</h2>
        <div className="grid grid-cols-2 gap-4">
          {deck.map((card, index) => (
            <Card key={index} className="relative">
              <CardContent className="p-2">
                <img src={card.img} alt={card.name} className="rounded-xl" />
                <p className="text-sm text-center mt-1">{card.name}</p>
                <Button
                  onClick={() => removeFromDeck(index)}
                  className="absolute top-1 right-1 px-1 py-0 text-xs"
                >
                  ✕
                </Button>
              </CardContent>
            </Card>
          ))}
        </div>
      </div>
    </div>
  );
}

