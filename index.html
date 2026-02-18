import React, { useState, useEffect, useRef } from 'react';
import { Heart, Plus, Ticket, Trash2, User, Sparkles, X, AlertCircle, Lock, Settings, LogOut, CheckCircle2, Bell } from 'lucide-react';
import { initializeApp } from "firebase/app";
import { getFirestore, doc, onSnapshot, setDoc, updateDoc, arrayUnion, getDoc } from "firebase/firestore";
import { getAuth, signInAnonymously } from "firebase/auth";

// --- FIREBASE CONFIGURATION ---
const firebaseConfig = {
  apiKey: "AIzaSyDnKHTghSxW7fi6bp_UGBhR6Nx4paAtO4U",
  authDomain: "my-babys-place.firebaseapp.com",
  projectId: "my-babys-place",
  storageBucket: "my-babys-place.firebasestorage.app",
  messagingSenderId: "276027805309",
  appId: "1:276027805309:web:7997b78ccf2c5004126b14",
  measurementId: "G-SX1LQK3CD8"
};

// Initialize Firebase
const app = initializeApp(firebaseConfig);
const db = getFirestore(app);
const auth = getAuth(app);

// Attempt anonymous login
signInAnonymously(auth).catch((err) => console.log("Auth note: Anon auth not enabled or needed.", err));

const ROOM_ID = "our_private_room"; // Single fixed room ID

const CATEGORIES = [
  { id: 'boobie', label: 'Boobie Ticket', icon: '🍒', color: 'from-pink-500 to-rose-500' },
  { id: 'ass', label: 'Ass Ticket', icon: '🍑', color: 'from-orange-400 to-red-500' },
  { id: 'pussy', label: 'Pussy Ticket', icon: '🐱', color: 'from-purple-500 to-indigo-500' },
  { id: 'fullbody', label: 'Full Body Ticket', icon: '🔥', color: 'from-red-500 to-pink-600' },
  { id: '1hour', label: '1 Hour Ticket', icon: '⏳', color: 'from-blue-400 to-cyan-500' },
  { id: 'nightshow', label: 'Night Show', icon: '🌙', color: 'from-indigo-600 to-purple-800' },
  { id: 'custom', label: 'Custom Wish', icon: '✨', color: 'from-emerald-400 to-teal-600' },
];

export default function App() {
  const [appState, setAppState] = useState('login'); // 'login' | 'dashboard'
  const [userMode, setUserMode] = useState(null); // 'creator' | 'user'
  const [tickets, setTickets] = useState([]);
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState('');
  
  // UI State
  const [showCreateModal, setShowCreateModal] = useState(false);
  const [showSettingsModal, setShowSettingsModal] = useState(false);
  const [activeTab, setActiveTab] = useState('wallet');
  const [redeemedTicket, setRedeemedTicket] = useState(null);

  // Notification State
  const prevTicketsRef = useRef([]);
  const isFirstLoad = useRef(true);

  // --- FIREBASE SYNC ---
  useEffect(() => {
    if (appState === 'dashboard') {
      setLoading(true);
      const docRef = doc(db, "love_wallets", ROOM_ID);
      
      const unsubscribe = onSnapshot(docRef, (docSnap) => {
        setLoading(false);
        if (docSnap.exists()) {
          const data = docSnap.data().tickets || [];
          setTickets(data.sort((a, b) => b.timestamp - a.timestamp));
        } else {
          setTickets([]); 
        }
      }, (err) => {
        console.error("Sync error:", err);
        setLoading(false);
        setError("Could not connect. Check internet.");
      });

      return () => unsubscribe();
    }
  }, [appState]);

  // --- NOTIFICATION LOGIC ---
  useEffect(() => {
    // Skip notification logic on initial load or if no user mode is set
    if (loading || !userMode) return;

    // On first true load with data, just set the ref and exit to avoid notification spam
    if (isFirstLoad.current) {
        prevTicketsRef.current = tickets;
        isFirstLoad.current = false;
        return;
    }

    const prevTickets = prevTicketsRef.current;

    // 1. Notify Boyfriend when a NEW ticket is created
    if (userMode === 'user') {
        const newTickets = tickets.filter(t => !prevTickets.find(p => p.id === t.id));
        newTickets.forEach(t => {
            if (Notification.permission === "granted") {
                 new Notification("New Love Ticket! 🎟️", { 
                    body: `She sent you: ${t.title}`,
                    icon: "https://cdn-icons-png.flaticon.com/512/2589/2589175.png" 
                 });
            }
        });
    }

    // 2. Notify Girlfriend when a ticket is REDEEMED
    if (userMode === 'creator') {
        const usedTickets = tickets.filter(t => t.status === 'used' && prevTickets.find(p => p.id === t.id && p.status === 'available'));
        usedTickets.forEach(t => {
            if (Notification.permission === "granted") {
                 new Notification("Ticket Redeemed! ✨", { 
                    body: `He used: ${t.title}`,
                    icon: "https://cdn-icons-png.flaticon.com/512/2589/2589175.png"
                 });
            }
        });
    }

    // Update ref for next run
    prevTicketsRef.current = tickets;
  }, [tickets, userMode, loading]);

  const handleRequestPermission = async () => {
    if (!("Notification" in window)) {
      alert("This browser does not support desktop notifications");
      return;
    }
    const permission = await Notification.requestPermission();
    if (permission === "granted") {
      new Notification("Notifications Enabled", { body: "You will now be notified of updates!" });
    } else {
      alert("Permission denied. Check your browser settings.");
    }
  };

  // --- ACTIONS ---

  const handleLogin = async (mode, pin) => {
    setLoading(true);
    setError('');

    const docRef = doc(db, "love_wallets", ROOM_ID);

    try {
      const docSnap = await getDoc(docRef);
      
      if (!docSnap.exists()) {
        if (pin !== '123') {
          setError("First time setup? Use default PIN: 123");
          setLoading(false);
          return;
        }
        await setDoc(docRef, { 
          tickets: [], 
          created: Date.now(),
          gfPin: '123',
          bfPin: '123'
        });
        setUserMode(mode);
        setAppState('dashboard');
      } else {
        const data = docSnap.data();
        const storedPin = mode === 'creator' ? (data.gfPin || '123') : (data.bfPin || '123');
        
        if (pin === storedPin) {
          setUserMode(mode);
          setAppState('dashboard');
        } else {
          setError("Incorrect PIN.");
        }
      }
    } catch (err) {
      console.error(err);
      setError("Connection failed.");
    }
    setLoading(false);
  };

  const handleCreate = async (newTicket) => {
    setShowCreateModal(false);
    try {
      const docRef = doc(db, "love_wallets", ROOM_ID);
      await updateDoc(docRef, {
        tickets: arrayUnion(newTicket)
      });
    } catch (err) {
      console.error("Error adding ticket:", err);
    }
  };

  const handleRedeem = async (id) => {
    const ticket = tickets.find(t => t.id === id);
    if (!ticket) return;

    setRedeemedTicket(ticket);
    setTimeout(() => setRedeemedTicket(null), 3000);

    try {
      const docRef = doc(db, "love_wallets", ROOM_ID);
      const updatedTickets = tickets.map(t => 
        t.id === id ? { ...t, status: 'used', usedAt: Date.now() } : t
      );
      await updateDoc(docRef, { tickets: updatedTickets });
    } catch (err) {
      console.error("Error redeeming:", err);
    }
  };

  const handleChangePin = async (newPin) => {
    try {
      const docRef = doc(db, "love_wallets", ROOM_ID);
      const field = userMode === 'creator' ? 'gfPin' : 'bfPin';
      await updateDoc(docRef, { [field]: newPin });
      alert("PIN updated successfully!");
      setShowSettingsModal(false);
    } catch (err) {
      alert("Failed to update PIN");
    }
  };

  const handleDelete = async (id) => {
    if (!confirm("Delete this ticket?")) return;
    try {
      const docRef = doc(db, "love_wallets", ROOM_ID);
      const updatedTickets = tickets.filter(t => t.id !== id);
      await updateDoc(docRef, { tickets: updatedTickets });
    } catch (err) {
      console.error("Error deleting:", err);
    }
  };

  // --- RENDER ---

  if (appState === 'login') {
    return <LoginScreen onLogin={handleLogin} error={error} loading={loading} />;
  }

  return (
    <div className="min-h-screen bg-slate-900 text-slate-100 font-sans selection:bg-pink-500 selection:text-white pb-20">
      {/* Header */}
      <header className="sticky top-0 z-10 bg-slate-900/80 backdrop-blur-md border-b border-white/10 p-4 flex justify-between items-center">
        <div className="flex items-center gap-2">
          <div className="bg-gradient-to-tr from-pink-500 to-purple-600 p-2 rounded-lg">
            <Ticket className="w-5 h-5 text-white" />
          </div>
          <div>
            <h1 className="font-bold text-lg bg-gradient-to-r from-pink-400 to-purple-400 bg-clip-text text-transparent">
              Love Tickets
            </h1>
          </div>
        </div>
        <div className="flex gap-2">
          <button 
            onClick={() => setShowSettingsModal(true)}
            className="p-2 rounded-full bg-white/5 hover:bg-white/10 text-slate-400"
          >
            <Settings className="w-4 h-4" />
          </button>
          <button 
            onClick={() => setAppState('login')}
            className="p-2 rounded-full bg-white/5 hover:bg-white/10 text-slate-400"
          >
            <LogOut className="w-4 h-4" />
          </button>
        </div>
      </header>

      {/* Main Content */}
      <main className="p-4 max-w-md mx-auto space-y-6">
        
        {loading && (
          <div className="text-center py-4 text-slate-500 animate-pulse text-sm">
            Syncing...
          </div>
        )}

        {/* Creator Controls */}
        {userMode === 'creator' && (
          <div className="bg-gradient-to-r from-slate-800 to-slate-800/50 p-6 rounded-2xl border border-white/5 shadow-xl relative overflow-hidden">
            <div className="absolute top-0 right-0 -mt-4 -mr-4 w-24 h-24 bg-pink-500/20 rounded-full blur-2xl"></div>
            <h2 className="text-lg font-semibold mb-2">Creator Dashboard</h2>
            <p className="text-slate-400 text-sm mb-4">Create new tickets for him to use.</p>
            <button 
              onClick={() => setShowCreateModal(true)}
              className="w-full py-3 bg-gradient-to-r from-pink-500 to-purple-600 rounded-xl font-bold flex items-center justify-center gap-2 shadow-lg shadow-pink-500/20 active:scale-95 transition-transform"
            >
              <Plus className="w-5 h-5" />
              Create New Ticket
            </button>
          </div>
        )}

        {/* User Stats / Tabs */}
        <div className="flex gap-4 p-1 bg-white/5 rounded-xl">
          <button 
            onClick={() => setActiveTab('wallet')}
            className={`flex-1 py-2 text-sm font-medium rounded-lg transition-all ${activeTab === 'wallet' ? 'bg-slate-700 text-white shadow-sm' : 'text-slate-400 hover:text-white'}`}
          >
            Wallet ({tickets.filter(t => t.status === 'available').length})
          </button>
          <button 
            onClick={() => setActiveTab('history')}
            className={`flex-1 py-2 text-sm font-medium rounded-lg transition-all ${activeTab === 'history' ? 'bg-slate-700 text-white shadow-sm' : 'text-slate-400 hover:text-white'}`}
          >
            History
          </button>
        </div>

        {/* Ticket Grid */}
        <div className="space-y-4">
          {tickets.filter(t => activeTab === 'wallet' ? t.status === 'available' : t.status === 'used').length === 0 ? (
            <div className="text-center py-12 opacity-50">
              <Ticket className="w-12 h-12 mx-auto mb-3 text-slate-600" />
              <p>No tickets found in {activeTab}</p>
              {userMode === 'creator' && activeTab === 'wallet' && <p className="text-xs text-slate-500 mt-2">Create one above!</p>}
            </div>
          ) : (
            tickets
              .filter(t => activeTab === 'wallet' ? t.status === 'available' : t.status === 'used')
              .map((ticket) => (
                <TicketCard 
                  key={ticket.id} 
                  ticket={ticket} 
                  userMode={userMode}
                  onRedeem={handleRedeem}
                  onDelete={handleDelete}
                />
              ))
          )}
        </div>
      </main>

      {/* Modals */}
      {showCreateModal && (
        <CreateTicketModal 
          onClose={() => setShowCreateModal(false)} 
          onCreate={handleCreate} 
        />
      )}

      {showSettingsModal && (
        <SettingsModal 
          onClose={() => setShowSettingsModal(false)} 
          onChangePin={handleChangePin}
          onEnableNotifications={handleRequestPermission}
          userMode={userMode}
        />
      )}

      {/* Redemption Celebration Overlay */}
      {redeemedTicket && (
        <div className="fixed inset-0 z-50 flex items-center justify-center bg-black/80 backdrop-blur-sm p-4 animate-in fade-in duration-300">
          <div className="bg-slate-900 border border-pink-500/50 p-8 rounded-3xl max-w-sm w-full text-center relative overflow-hidden shadow-2xl shadow-pink-500/30">
            <div className="absolute inset-0 bg-gradient-to-b from-pink-500/10 to-transparent"></div>
            <Sparkles className="w-16 h-16 text-pink-400 mx-auto mb-4 animate-bounce" />
            <h2 className="text-3xl font-bold bg-gradient-to-r from-pink-400 to-purple-400 bg-clip-text text-transparent mb-2">
              Redeemed!
            </h2>
            <p className="text-slate-300 mb-6">
              You have used: <br/>
              <span className="font-semibold text-white text-lg">{redeemedTicket.title}</span>
            </p>
            <div className="text-xs text-slate-500 uppercase tracking-widest">Enjoy your time</div>
          </div>
        </div>
      )}
    </div>
  );
}

// --- Sub Components ---

function LoginScreen({ onLogin, error, loading }) {
  const [pin, setPin] = useState('');
  const [selectedRole, setSelectedRole] = useState(null); // 'creator' | 'user'

  const handleSubmit = (e) => {
    e.preventDefault();
    if (selectedRole && pin) {
      onLogin(selectedRole, pin);
    }
  };

  return (
    <div className="min-h-screen bg-slate-950 flex flex-col items-center justify-center p-6 text-center relative overflow-hidden">
      <div className="absolute top-10 left-10 w-64 h-64 bg-purple-600/20 rounded-full blur-[100px]"></div>
      <div className="absolute bottom-10 right-10 w-64 h-64 bg-pink-600/20 rounded-full blur-[100px]"></div>

      <div className="mb-6 relative z-10">
        <div className="bg-gradient-to-tr from-pink-500 to-purple-600 p-4 rounded-2xl shadow-2xl shadow-pink-500/20 transform rotate-3 mx-auto w-fit">
          <Heart className="w-8 h-8 text-white fill-white" />
        </div>
      </div>
      
      <h1 className="text-3xl font-black text-white mb-2 tracking-tight">Love Tickets</h1>
      <p className="text-slate-400 mb-8 max-w-xs text-sm">Select your identity to enter.</p>

      {error && (
        <div className="bg-red-500/10 border border-red-500/20 p-3 rounded-lg text-red-400 text-xs mb-4 flex items-center gap-2">
          <AlertCircle className="w-4 h-4" /> {error}
        </div>
      )}

      <form onSubmit={handleSubmit} className="w-full max-w-xs space-y-4">
        
        {/* Role Selection */}
        <div className="grid grid-cols-2 gap-4">
          <button 
            type="button"
            onClick={() => setSelectedRole('creator')}
            className={`p-4 rounded-2xl border-2 transition-all text-xs font-bold flex flex-col items-center gap-3 relative overflow-hidden group
              ${selectedRole === 'creator' 
                ? 'bg-pink-500/10 border-pink-500 text-pink-400 shadow-[0_0_20px_rgba(236,72,153,0.3)]' 
                : 'bg-slate-900 border-slate-800 text-slate-500 hover:border-slate-700 hover:bg-slate-800'}`}
          >
            <Sparkles className={`w-8 h-8 ${selectedRole === 'creator' ? 'text-pink-400' : 'text-slate-600 group-hover:text-slate-400'}`} />
            <span className="uppercase tracking-wide">Girlfriend</span>
            {selectedRole === 'creator' && <div className="absolute top-2 right-2 w-2 h-2 bg-pink-500 rounded-full animate-pulse"></div>}
          </button>

          <button 
             type="button"
             onClick={() => setSelectedRole('user')}
             className={`p-4 rounded-2xl border-2 transition-all text-xs font-bold flex flex-col items-center gap-3 relative overflow-hidden group
               ${selectedRole === 'user' 
                 ? 'bg-blue-500/10 border-blue-500 text-blue-400 shadow-[0_0_20px_rgba(59,130,246,0.3)]' 
                 : 'bg-slate-900 border-slate-800 text-slate-500 hover:border-slate-700 hover:bg-slate-800'}`}
          >
            <User className={`w-8 h-8 ${selectedRole === 'user' ? 'text-blue-400' : 'text-slate-600 group-hover:text-slate-400'}`} />
            <span className="uppercase tracking-wide">Boyfriend</span>
            {selectedRole === 'user' && <div className="absolute top-2 right-2 w-2 h-2 bg-blue-500 rounded-full animate-pulse"></div>}
          </button>
        </div>

        {/* PIN Entry (Only shows after role selected) */}
        {selectedRole && (
          <div className="animate-in slide-in-from-bottom-4 fade-in duration-300 pt-2">
             <div className="text-center mb-2">
              <label className="text-[10px] font-bold text-slate-500 uppercase tracking-widest">
                Enter PIN for {selectedRole === 'creator' ? 'Her' : 'Him'}
              </label>
             </div>
             <div className="relative">
                <input 
                  type="password" 
                  autoFocus
                  placeholder="PIN (Default: 123)"
                  className="w-full bg-slate-900 border border-white/10 rounded-xl p-4 text-center text-white font-bold tracking-[0.5em] text-lg focus:border-pink-500 focus:outline-none focus:ring-1 focus:ring-pink-500/50 transition-all placeholder:tracking-normal placeholder:font-normal placeholder:text-sm placeholder:text-slate-700"
                  value={pin}
                  onChange={(e) => setPin(e.target.value)}
                />
             </div>
             
             <button 
                type="submit"
                disabled={!pin || loading}
                className="w-full mt-4 py-3 bg-gradient-to-r from-pink-500 to-purple-600 rounded-xl font-bold text-white shadow-lg active:scale-95 transition-all disabled:opacity-50 hover:shadow-pink-500/25"
              >
                {loading ? 'Unlocking...' : 'Unlock Wallet'}
              </button>
          </div>
        )}
      </form>
    </div>
  );
}

function SettingsModal({ onClose, onChangePin, onEnableNotifications, userMode }) {
  const [newPin, setNewPin] = useState('');

  const handleSubmit = (e) => {
    e.preventDefault();
    if (newPin.length > 0) onChangePin(newPin);
  };

  return (
    <div className="fixed inset-0 z-50 flex items-center justify-center bg-black/80 backdrop-blur-sm p-4">
      <div className="bg-slate-900 border border-white/10 rounded-2xl w-full max-w-xs p-6 relative">
        <button onClick={onClose} className="absolute top-4 right-4 text-slate-500 hover:text-white"><X className="w-4 h-4" /></button>
        <h3 className="text-lg font-bold mb-4">Settings</h3>
        
        <div className="mb-6">
          <label className="text-[10px] font-bold text-slate-500 uppercase mb-2 block">Notifications</label>
          <button 
            onClick={onEnableNotifications}
            className="w-full py-3 bg-slate-800 hover:bg-slate-700 border border-white/5 rounded-xl flex items-center justify-center gap-2 text-sm font-medium transition-all"
          >
            <Bell className="w-4 h-4 text-pink-400" />
            Enable Notifications
          </button>
          <p className="text-[10px] text-slate-500 mt-2 text-center">
            Allows the app to notify you even when in the background (keep tab open).
          </p>
        </div>

        <div className="border-t border-white/10 pt-4">
          <label className="text-[10px] font-bold text-slate-500 uppercase mb-2 block">Security</label>
          <p className="text-slate-400 text-xs mb-3">Change PIN for {userMode === 'creator' ? 'Girlfriend' : 'Boyfriend'}</p>
          
          <form onSubmit={handleSubmit}>
            <input 
              type="text" 
              className="w-full bg-slate-950 border border-white/10 rounded-xl p-3 text-white mb-3 focus:border-pink-500 focus:outline-none"
              value={newPin}
              onChange={(e) => setNewPin(e.target.value)}
              placeholder="Enter new PIN"
            />
            <button type="submit" className="w-full py-2 bg-pink-600 hover:bg-pink-500 rounded-lg text-sm font-bold text-white transition-colors">
              Update PIN
            </button>
          </form>
        </div>
      </div>
    </div>
  );
}

function TicketCard({ ticket, userMode, onRedeem, onDelete }) {
  const category = CATEGORIES.find(c => c.id === ticket.type) || CATEGORIES[6];
  const isUsed = ticket.status === 'used';
  
  return (
    <div className={`relative group ${isUsed ? 'opacity-60 grayscale' : ''}`}>
      <div className={`
        relative overflow-hidden rounded-2xl p-5 
        bg-gradient-to-br ${isUsed ? 'from-slate-800 to-slate-900' : 'from-slate-800 to-slate-900'} 
        border ${isUsed ? 'border-slate-700' : 'border-white/10'}
        shadow-xl transition-all
      `}>
        <div className={`absolute left-0 top-0 bottom-0 w-1.5 bg-gradient-to-b ${category.color} ${isUsed ? 'opacity-30' : ''}`}></div>

        <div className="flex justify-between items-start pl-3">
          <div className="flex-1">
            <div className="flex items-center gap-2 mb-1">
              <span className="text-2xl">{category.icon}</span>
              <span className={`text-[10px] font-bold px-2 py-0.5 rounded-full bg-white/5 text-slate-300 border border-white/5`}>
                {category.label}
              </span>
            </div>
            <h3 className="text-lg font-bold text-white leading-tight">{ticket.title}</h3>
            <p className="text-slate-400 text-sm mt-1">{ticket.description}</p>
            {isUsed && (
               <p className="text-slate-600 text-xs mt-2 flex items-center gap-1"><CheckCircle2 className="w-3 h-3"/> Used on {new Date(ticket.usedAt).toLocaleDateString()}</p>
            )}
          </div>
          
          {userMode === 'creator' && (
            <button 
              onClick={() => onDelete(ticket.id)}
              className="p-2 ml-2 text-slate-600 hover:text-red-400 transition-colors"
            >
              <Trash2 className="w-4 h-4" />
            </button>
          )}

          {isUsed && userMode !== 'creator' && (
            <div className="ml-2 px-3 py-1 bg-slate-800 rounded-full border border-slate-700 whitespace-nowrap">
               <span className="text-xs font-bold text-slate-500">USED</span>
            </div>
          )}
        </div>

        {userMode === 'user' && !isUsed && (
          <div className="mt-4 pl-3">
            <button 
              onClick={() => onRedeem(ticket.id)}
              className={`
                w-full py-2.5 rounded-xl text-sm font-bold flex items-center justify-center gap-2
                bg-gradient-to-r ${category.color} text-white shadow-lg
                hover:opacity-90 active:scale-[0.98] transition-all
              `}
            >
              <Ticket className="w-4 h-4" />
              Redeem Ticket
            </button>
          </div>
        )}
      </div>
    </div>
  );
}

function CreateTicketModal({ onClose, onCreate }) {
  const [selectedCat, setSelectedCat] = useState(CATEGORIES[0]);
  const [customTitle, setCustomTitle] = useState('');
  const [description, setDescription] = useState('');

  const handleSubmit = (e) => {
    e.preventDefault();
    const newTicket = {
      id: crypto.randomUUID(),
      type: selectedCat.id,
      title: selectedCat.id === 'custom' ? customTitle : selectedCat.label,
      description: description || 'No rules, just love.',
      status: 'available',
      timestamp: Date.now(),
    };
    onCreate(newTicket);
  };

  return (
    <div className="fixed inset-0 z-50 flex items-center justify-center bg-black/80 backdrop-blur-sm p-4">
      <div className="bg-slate-900 border border-white/10 rounded-2xl w-full max-w-md overflow-hidden flex flex-col max-h-[90vh]">
        <div className="p-4 border-b border-white/10 flex justify-between items-center">
          <h3 className="font-bold text-lg">Create New Ticket</h3>
          <button onClick={onClose} className="p-1 hover:bg-white/10 rounded-full"><X className="w-5 h-5" /></button>
        </div>

        <div className="p-4 overflow-y-auto">
          <div className="mb-6">
            <label className="text-xs font-bold text-slate-400 uppercase mb-3 block">Choose Category</label>
            <div className="grid grid-cols-2 gap-2">
              {CATEGORIES.map(cat => (
                <button
                  key={cat.id}
                  type="button"
                  onClick={() => setSelectedCat(cat)}
                  className={`
                    flex items-center gap-2 p-3 rounded-xl border text-sm font-medium transition-all text-left
                    ${selectedCat.id === cat.id 
                      ? 'bg-slate-800 border-pink-500 text-white shadow-lg shadow-pink-500/10' 
                      : 'bg-slate-800/50 border-transparent hover:bg-slate-800 text-slate-400'}
                  `}
                >
                  <span>{cat.icon}</span>
                  <span>{cat.label}</span>
                </button>
              ))}
            </div>
          </div>

          <form onSubmit={handleSubmit} className="space-y-4">
            {selectedCat.id === 'custom' && (
              <div>
                <label className="text-xs font-bold text-slate-400 uppercase mb-1 block">Title</label>
                <input 
                  type="text" 
                  required
                  placeholder="e.g. Breakfast in Bed"
                  className="w-full bg-slate-950 border border-white/10 rounded-xl p-3 text-white focus:border-pink-500 focus:outline-none"
                  value={customTitle}
                  onChange={(e) => setCustomTitle(e.target.value)}
                />
              </div>
            )}

            <div>
              <label className="text-xs font-bold text-slate-400 uppercase mb-1 block">Description / Rules</label>
              <textarea 
                rows="3"
                placeholder="What does this ticket grant him? Any conditions?"
                className="w-full bg-slate-950 border border-white/10 rounded-xl p-3 text-white focus:border-pink-500 focus:outline-none resize-none"
                value={description}
                onChange={(e) => setDescription(e.target.value)}
              />
            </div>

            <button 
              type="submit"
              className="w-full py-4 bg-gradient-to-r from-pink-500 to-purple-600 rounded-xl font-bold text-white shadow-lg shadow-pink-500/25 active:scale-95 transition-transform"
            >
              Mint Ticket
            </button>
          </form>
        </div>
      </div>
    </div>
  );
}
