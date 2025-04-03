import React, { useState } from "react";

const actions = { "gol": 5, "cade": 10, "completo squadra": 10, "outfit og": 10, "casca": 20, "ospedale": 100, "sangue": 15, "migliore": 20, "insulti": 30, "complimenti": 2, "allenatore": 10, "scarpa og": 5, "mani addosso": 50, "risata gruppo": 5, "beve": 2, "parata": 5, "colpo palle": 15, "rientra in campo": 15, "tunnel fatto": 5, "fa cadere": -10, "no vestiti squadra": -5, "morto": -10, "riposo": -10, "allaccia scarpa": -5, "urla": -5, "pianto": -20, "palla addosso": -50, "scazzo palla": -20, "palo": -10, "liscio": -15, "palla incastrata": -10, "rompono qualcosa": -25, "pacco": -75, "non ride": -5, "sputi": -20, "colpo dato palle": -10, "gol ricevuto": -5, "tunnel ricevuto": -5, "scelta ora sbagliata": -15 };

function GameScoreTracker() { const [players, setPlayers] = useState([]); const [scores, setScores] = useState({}); const [playerName, setPlayerName] = useState(""); const [selectedPlayer, setSelectedPlayer] = useState(""); const [selectedAction, setSelectedAction] = useState("");

const addPlayer = () => { if (playerName && !players.includes(playerName)) { setPlayers([...players, playerName]); setScores({ ...scores, [playerName]: 0 }); setPlayerName(""); } };

const addAction = () => { if (selectedPlayer && selectedAction) { setScores(prevScores => ({ ...prevScores, [selectedPlayer]: (prevScores[selectedPlayer] || 0) + actions[selectedAction] })); setSelectedAction(""); } };

return ( <div className="p-4 max-w-lg mx-auto bg-gray-100 shadow-lg rounded-lg"> <h1 className="text-xl font-bold mb-4">Game Score Tracker</h1>

<div className="mb-4">
    <input value={playerName} onChange={(e) => setPlayerName(e.target.value)} placeholder="Nome giocatore" className="border p-2 mr-2" />
    <button onClick={addPlayer} className="bg-blue-500 text-white p-2">Aggiungi</button>
  </div>
  
  {players.length > 0 && (
    <div className="mb-4">
      <select value={selectedPlayer} onChange={(e) => setSelectedPlayer(e.target.value)} className="border p-2">
        <option value="">Seleziona un giocatore</option>
        {players.map(player => <option key={player} value={player}>{player}</option>)}
      </select>
      <select value={selectedAction} onChange={(e) => setSelectedAction(e.target.value)} className="border p-2 mx-2">
        <option value="">Seleziona un'azione</option>
        {Object.keys(actions).map(action => <option key={action} value={action}>{action} ({actions[action]})</option>)}
      </select>
      <button onClick={addAction} className="bg-green-500 text-white p-2">Aggiungi azione</button>
    </div>
  )}
  
  <h2 className="text-lg font-bold">Punteggi:</h2>
  <ul>
    {players.map(player => (
      <li key={player} className="border-b p-2">{player}: {scores[player]}</li>
    ))}
  </ul>
</div>

); }

export default GameScoreTracker;

