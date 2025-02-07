import { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { motion } from "framer-motion";
import { FaHeart } from "react-icons/fa";

const dateSpots = [
  { id: 1, name: "Rooftop Dinner at Bustle", description: "A luxurious rooftop dinner experience with a stunning view.", address: "Rike Terrace Bar & Grill, Veera Desai Area, Mumbai", time: "11:00 PM on 11th Feb", image: "/images/rooftop_dinner.jpg" },
  { id: 2, name: "Sea View Dining at Bora Bora", description: "A cozy sea-facing restaurant with a beautiful ambiance.", address: "Bora Bora, Juhu, Mumbai", time: "6:30 PM on 9th Feb", image: "/images/bora_bora.jpg" },
  { id: 3, name: "Sea View Dining at Razzberry Rhinoceros", description: "A romantic dining experience with an ocean view.", address: "Razzberry Rhinoceros, Juhu, Mumbai", time: "11:30 PM on 11th Feb", image: "/images/razzberry_rhinoceros.jpg" },
  { id: 4, name: "Candlelight Dinner at Que Sera Sera", description: "A romantic candlelight dinner experience in an intimate setting.", address: "Que Sera Sera, Andheri, Mumbai", time: "11:00 PM on 11th Feb", image: "/images/que_sera_sera.jpg" },
  { id: 5, name: "Pizza at Pass The Salt", description: "A delightful pizza experience at a cozy spot.", address: "Pass The Salt, Fort, Mumbai", time: "2:00 PM on 11th Feb", image: "/images/pass_the_salt.jpg" },
  { id: 6, name: "Dinner at Madeira & Mime", description: "A unique dining experience with a lively ambiance.", address: "Madeira & Mime, Powai, Mumbai", time: "8:30 PM on 11th Feb", image: "/images/madeira_mime.jpg" },
  { id: 7, name: "Luxury Dining at Era", description: "A premium dining experience with an elegant ambiance.", address: "Era, Veera Desai Area, Mumbai", time: "6:30 PM on 9th Feb or 11:00 PM on 11th Feb", image: "/images/era.jpg" },
  { id: 8, name: "Luxury Dining at Akina", description: "An exquisite fine dining experience with a luxurious ambiance.", address: "Akina, Linking Road, Bandra, Mumbai", time: "11:30 PM on 11th Feb", image: "/images/akina.jpg" },
  { id: 9, name: "Luxury Dining at Bawri", description: "A refined dining experience with a blend of modern and traditional flavors.", address: "Bawri, BKC, Mumbai", time: "2:30 PM on 9th Feb", image: "/images/bawri.jpg" },
  { id: 10, name: "End of the Night with Ice Cream", description: "A sweet ending to our special day, enjoying your favorite ice cream while strolling by the sea.", address: "Marine Drive or Coastal Road, Mumbai", time: "After dinner", image: "/images/ice_cream.jpg" }
];

export default function DatePlanner() {
  const [selectedSpots, setSelectedSpots] = useState([]);
  const [confirmed, setConfirmed] = useState(false);
  const [selectedLocation, setSelectedLocation] = useState(null);

  const toggleSpot = (spot) => {
    setSelectedSpots((prev) =>
      prev.includes(spot)
        ? prev.filter((s) => s !== spot)
        : [...prev, spot]
    );
  };

  return (
    <div className="min-h-screen bg-pink-200 flex flex-col items-center p-6 text-center">
      <motion.h1 className="text-4xl font-bold text-red-500" animate={{ scale: 1.1 }}>
        Plan Our Perfect Date ❤️
      </motion.h1>
      <p className="mt-4 text-lg text-gray-700">
        If you have another place in mind, let me know! We can go anywhere you like, but one thing is for sure – we're going on this special date together, and it's going to be magical. 💖
      </p>
      <div className="grid grid-cols-1 md:grid-cols-2 gap-4 mt-6">
        {dateSpots.map((spot) => (
          <motion.div key={spot.id} whileHover={{ scale: 1.05 }}>
            <Card
              className={`p-4 cursor-pointer ${selectedSpots.includes(spot) ? "bg-red-300" : "bg-white"}`}
              onClick={() => setSelectedLocation(spot)}
            >
              <CardContent>
                <h2 className="text-xl font-semibold">{spot.name}</h2>
                <p className="text-gray-600">{spot.description}</p>
              </CardContent>
            </Card>
          </motion.div>
        ))}
      </div>
      <Button
        className="mt-6 bg-red-500 text-white p-3 rounded-full"
        onClick={() => setConfirmed(true)}
      >
        Confirm Plan <FaHeart className="ml-2" />
      </Button>
      {confirmed && (
        <motion.div className="mt-6 p-4 bg-white rounded-xl shadow-lg" animate={{ opacity: 1 }}>
          <h2 className="text-2xl font-bold text-red-500">Your Date Plan ❤️</h2>
          <ul className="mt-2">
            {selectedSpots.map((spot, index) => (
              <li key={index} className="text-lg text-gray-700">- {spot.name}</li>
            ))}
          </ul>
        </motion.div>
      )}
      {selectedLocation && (
        <motion.div className="mt-6 p-6 bg-white rounded-xl shadow-lg text-center" animate={{ opacity: 1 }}>
          <h2 className="text-2xl font-bold text-red-500">{selectedLocation.name}</h2>
          <img src={selectedLocation.image} alt={selectedLocation.name} className="w-full h-48 object-cover mt-2 rounded-lg" />
          <p className="text-gray-700 mt-2">{selectedLocation.description}</p>
          <p className="text-gray-600 mt-1">📍 {selectedLocation.address}</p>
          <p className="text-gray-600">⏰ {selectedLocation.time}</p>
          <Button className="mt-4 bg-red-400 text-white p-2 rounded" onClick={() => setSelectedLocation(null)}>
            Close
          </Button>
        </motion.div>
      )}
    </div>
  );
}
