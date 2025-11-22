# oktat-s
import React, { useState, useRef, useEffect } from 'react';
import { 
  BookOpen, 
  FileText, 
  Upload, 
  Send, 
  Cpu, 
  CheckCircle, 
  Brain, 
  ChevronRight, 
  MessageSquare, 
  X,
  Sparkles,
  ArrowRight,
  Image as ImageIcon,
  Video,
  Wand2,
  Download,
  PlayCircle
} from 'lucide-react';

// --- Mock AI Szimulációs Logika ---
const simulateAIResponse = (message) => {
  const lowerMsg = message.toLowerCase();
  if (lowerMsg.includes("szia") || lowerMsg.includes("helló")) return "Szia! Miben segíthetek ma a tanulásban, dokumentum elemzésben vagy média generálásban?";
  if (lowerMsg.includes("magyarázd el")) return "Természetesen. A kért fogalom lényege, hogy egyszerűsítsük a komplex információkat. Képzeld el úgy, mint egy tolmácsot a szaknyelv és a hétköznapi beszéd között.";
  if (lowerMsg.includes("történelem")) return "A történelem tele van izgalmas eseményekkel. Szeretnél egy konkrét korszakról hallani, vagy inkább összefüggéseket keresel?";
  if (lowerMsg.includes("matek") || lowerMsg.includes("matematika")) return "A matematika a logika nyelve. Van egy konkrét példa, amit nem értesz, vagy az alapokkal kezdjük?";
  return "Ez egy érdekes kérdés! Az AI modellem elemzi a kontextust. Röviden: a téma összetett, de lépésről lépésre megérthetjük. Szeretnéd, ha részletesebben kifejteném?";
};

const simulateDocAnalysis = () => {
  return `DOKUMENTUM ÖSSZEFOGLALÓ:
  
1. Fő téma: A feltöltött dokumentum a fenntartható energiaforrások gazdasági hatásait tárgyalja a következő 5 évre vetítve.
  
2. Kulcspontok:
   - A napenergia költségei 15%-kal csökkenhetnek.
   - Új támogatási rendszerek várhatók a lakossági szektorban.
   - A fosszilis tüzelőanyagok adóztatása szigorodik.

3. Következtetés: Érdemes most beruházni a megújuló rendszerekbe, mivel a megtérülési idő 2 évvel rövidült az előző elemzésekhez képest.
  
(Ez egy generált minta szöveg a demonstrációhoz.)`;
};

export default function TudasTarsApp() {
  const [activeTab, setActiveTab] = useState('home'); // 'home', 'edu', 'doc', 'media'
  const [isMenuOpen, setIsMenuOpen] = useState(false);

  // --- Navigáció ---
  const renderContent = () => {
    switch (activeTab) {
      case 'home': return <HeroSection setActiveTab={setActiveTab} />;
      case 'edu': return <EducationModule />;
      case 'doc': return <DocumentAnalysisModule />;
      case 'media': return <MediaGeneratorModule />;
      default: return <HeroSection setActiveTab={setActiveTab} />;
    }
  };

  return (
    <div className="min-h-screen bg-slate-50 text-slate-800 font-sans selection:bg-indigo-100 selection:text-indigo-900">
      {/* Fejléc */}
      <nav className="bg-white shadow-sm sticky top-0 z-50 border-b border-slate-100">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="flex justify-between h-16">
            <div className="flex items-center cursor-pointer" onClick={() => setActiveTab('home')}>
              <div className="bg-indigo-600 p-2 rounded-lg mr-2">
                <Brain className="h-6 w-6 text-white" />
              </div>
              <span className="text-xl font-bold text-slate-900 tracking-tight">Tudás<span className="text-indigo-600">Társ</span></span>
            </div>
            
            {/* Desktop Menu */}
            <div className="hidden md:flex space-x-8 items-center">
              <button 
                onClick={() => setActiveTab('home')}
                className={`px-3 py-2 rounded-md text-sm font-medium transition-colors ${activeTab === 'home' ? 'text-indigo-600 bg-indigo-50' : 'text-slate-600 hover:text-indigo-600'}`}
              >
                Kezdőlap
              </button>
              <button 
                onClick={() => setActiveTab('edu')}
                className={`px-3 py-2 rounded-md text-sm font-medium transition-colors ${activeTab === 'edu' ? 'text-indigo-600 bg-indigo-50' : 'text-slate-600 hover:text-indigo-600'}`}
              >
                AI Oktató
              </button>
              <button 
                onClick={() => setActiveTab('doc')}
                className={`px-3 py-2 rounded-md text-sm font-medium transition-colors ${activeTab === 'doc' ? 'text-indigo-600 bg-indigo-50' : 'text-slate-600 hover:text-indigo-600'}`}
              >
                Dokumentum Elemző
              </button>
              <button 
                onClick={() => setActiveTab('media')}
                className={`px-3 py-2 rounded-md text-sm font-medium transition-colors ${activeTab === 'media' ? 'text-indigo-600 bg-indigo-50' : 'text-slate-600 hover:text-indigo-600'}`}
              >
                Média Stúdió
              </button>
            </div>

            {/* Mobile Menu Button */}
            <div className="md:hidden flex items-center">
              <button onClick={() => setIsMenuOpen(!isMenuOpen)} className="text-slate-500 hover:text-slate-700">
                <span className="sr-only">Menü megnyitása</span>
                <svg className="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M4 6h16M4 12h16M4 18h16" />
                </svg>
              </button>
            </div>
          </div>
        </div>
        
        {/* Mobile Menu Dropdown */}
        {isMenuOpen && (
          <div className="md:hidden bg-white border-b border-slate-100">
            <div className="px-2 pt-2 pb-3 space-y-1 sm:px-3">
              <button onClick={() => {setActiveTab('home'); setIsMenuOpen(false)}} className="block w-full text-left px-3 py-2 rounded-md text-base font-medium text-slate-700 hover:text-indigo-600 hover:bg-slate-50">Kezdőlap</button>
              <button onClick={() => {setActiveTab('edu'); setIsMenuOpen(false)}} className="block w-full text-left px-3 py-2 rounded-md text-base font-medium text-slate-700 hover:text-indigo-600 hover:bg-slate-50">AI Oktató</button>
              <button onClick={() => {setActiveTab('doc'); setIsMenuOpen(false)}} className="block w-full text-left px-3 py-2 rounded-md text-base font-medium text-slate-700 hover:text-indigo-600 hover:bg-slate-50">Dokumentum Elemző</button>
              <button onClick={() => {setActiveTab('media'); setIsMenuOpen(false)}} className="block w-full text-left px-3 py-2 rounded-md text-base font-medium text-slate-700 hover:text-indigo-600 hover:bg-slate-50">Média Stúdió</button>
            </div>
          </div>
        )}
      </nav>

      {/* Fő Tartalom */}
      <main>
        {renderContent()}
      </main>

      {/* Lábléc */}
      <footer className="bg-white border-t border-slate-200 py-8 mt-12">
        <div className="max-w-7xl mx-auto px-4 text-center text-slate-500 text-sm">
          <p>&copy; 2024 TudásTárs AI. Minden jog fenntartva.</p>
          <p className="mt-2">Az AI oktatás, dokumentum feldolgozás és média generálás egyszerűsítve.</p>
        </div>
      </footer>
    </div>
  );
}

// --- Komponens: Kezdőlap (Hero) ---
function HeroSection({ setActiveTab }) {
  return (
    <div className="relative overflow-hidden">
      <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-16 sm:py-24">
        <div className="text-center">
          <div className="inline-flex items-center px-4 py-2 rounded-full bg-indigo-100 text-indigo-800 text-sm font-semibold mb-6">
            <Sparkles className="w-4 h-4 mr-2" />
            Mesterséges Intelligencia mindenkinek
          </div>
          <h1 className="text-4xl sm:text-5xl md:text-6xl font-extrabold text-slate-900 tracking-tight mb-6">
            Tanulj, elemezz és<br />
            <span className="text-indigo-600">alkoss szabadon.</span>
          </h1>
          <p className="mt-4 max-w-2xl mx-auto text-xl text-slate-600 mb-10">
            A TudásTárs segít egyszerű nyelven elmagyarázni bonyolult témákat, összefoglalja a dokumentumaidat, és most már <strong>képeket és videókat</strong> is generál neked.
          </p>
          <div className="flex flex-col sm:flex-row justify-center gap-4">
            <button 
              onClick={() => setActiveTab('edu')}
              className="inline-flex items-center justify-center px-8 py-3 border border-transparent text-base font-medium rounded-lg text-white bg-indigo-600 hover:bg-indigo-700 md:text-lg shadow-lg shadow-indigo-200 transition-all transform hover:-translate-y-1"
            >
              <BookOpen className="w-5 h-5 mr-2" />
              Tanulás indítása
            </button>
            <button 
              onClick={() => setActiveTab('media')}
              className="inline-flex items-center justify-center px-8 py-3 border border-indigo-200 text-base font-medium rounded-lg text-indigo-700 bg-indigo-50 hover:bg-indigo-100 md:text-lg shadow-sm transition-all"
            >
              <Wand2 className="w-5 h-5 mr-2" />
              Média Generálás
            </button>
          </div>
        </div>

        {/* Feature Cards */}
        <div className="mt-20 grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
          <div className="bg-white p-6 rounded-xl shadow-sm border border-slate-100 hover:shadow-md transition-shadow">
            <div className="w-12 h-12 bg-blue-100 rounded-lg flex items-center justify-center mb-4">
              <MessageSquare className="w-6 h-6 text-blue-600" />
            </div>
            <h3 className="text-lg font-bold text-slate-900 mb-2">Türelmes Oktató</h3>
            <p className="text-slate-600 text-sm">Kérdezz bármit. Az AI addig magyarázza, amíg meg nem érted, egyszerű példákkal.</p>
          </div>
          <div className="bg-white p-6 rounded-xl shadow-sm border border-slate-100 hover:shadow-md transition-shadow">
            <div className="w-12 h-12 bg-green-100 rounded-lg flex items-center justify-center mb-4">
              <FileText className="w-6 h-6 text-green-600" />
            </div>
            <h3 className="text-lg font-bold text-slate-900 mb-2">Jogi Bikkfanyelv?</h3>
            <p className="text-slate-600 text-sm">Nem érted a szerződést? Töltsd fel, és mi lefordítjuk "emberi nyelvre".</p>
          </div>
          <div className="bg-white p-6 rounded-xl shadow-sm border border-slate-100 hover:shadow-md transition-shadow">
            <div className="w-12 h-12 bg-purple-100 rounded-lg flex items-center justify-center mb-4">
              <Cpu className="w-6 h-6 text-purple-600" />
            </div>
            <h3 className="text-lg font-bold text-slate-900 mb-2">Azonnali Elemzés</h3>
            <p className="text-slate-600 text-sm">Nincs várakozás. A technológia másodpercek alatt feldolgozza az információt.</p>
          </div>
          <div className="bg-white p-6 rounded-xl shadow-sm border border-slate-100 hover:shadow-md transition-shadow">
            <div className="w-12 h-12 bg-pink-100 rounded-lg flex items-center justify-center mb-4">
              <Wand2 className="w-6 h-6 text-pink-600" />
            </div>
            <h3 className="text-lg font-bold text-slate-900 mb-2">Média Alkotás</h3>
            <p className="text-slate-600 text-sm">Készíts egyedi illusztrációkat és rövid videókat egyszerű szöveges leírásból.</p>
          </div>
        </div>
      </div>
    </div>
  );
}

// --- Komponens: Oktató Modul (Chat) ---
function EducationModule() {
  const [messages, setMessages] = useState([
    { id: 1, sender: 'ai', text: 'Szia! Én vagyok az AI oktatód. Mi az a téma, ami mostanában nehézséget okoz, vagy amiről többet szeretnél tudni? (pl. Történelem, Matek, Biológia)' }
  ]);
  const [input, setInput] = useState('');
  const [isTyping, setIsTyping] = useState(false);
  const messagesEndRef = useRef(null);

  const scrollToBottom = () => {
    messagesEndRef.current?.scrollIntoView({ behavior: "smooth" });
  };

  useEffect(() => {
    scrollToBottom();
  }, [messages, isTyping]);

  const handleSend = () => {
    if (!input.trim()) return;

    // User message
    const newMsg = { id: Date.now(), sender: 'user', text: input };
    setMessages(prev => [...prev, newMsg]);
    setInput('');
    setIsTyping(true);

    // AI Response Simulation
    setTimeout(() => {
      const responseText = simulateAIResponse(newMsg.text);
      setMessages(prev => [...prev, { id: Date.now() + 1, sender: 'ai', text: responseText }]);
      setIsTyping(false);
    }, 1500);
  };

  return (
    <div className="max-w-4xl mx-auto px-4 py-8 h-[calc(100vh-140px)] flex flex-col">
      <div className="bg-white rounded-2xl shadow-lg border border-slate-200 flex flex-col h-full overflow-hidden">
        {/* Chat Header */}
        <div className="bg-indigo-600 p-4 flex items-center text-white">
          <div className="bg-indigo-500 p-2 rounded-full mr-3">
            <BookOpen className="w-5 h-5" />
          </div>
          <div>
            <h2 className="font-bold text-lg">Személyes AI Tanár</h2>
            <p className="text-indigo-200 text-xs">Mindig elérhető, végtelenül türelmes</p>
          </div>
        </div>

        {/* Chat Messages */}
        <div className="flex-1 overflow-y-auto p-4 space-y-4 bg-slate-50">
          {messages.map((msg) => (
            <div key={msg.id} className={`flex ${msg.sender === 'user' ? 'justify-end' : 'justify-start'}`}>
              <div className={`max-w-[80%] p-4 rounded-2xl text-sm sm:text-base leading-relaxed shadow-sm ${
                msg.sender === 'user' 
                  ? 'bg-indigo-600 text-white rounded-br-none' 
                  : 'bg-white text-slate-800 border border-slate-200 rounded-bl-none'
              }`}>
                {msg.text}
              </div>
            </div>
          ))}
          {isTyping && (
            <div className="flex justify-start">
              <div className="bg-white p-4 rounded-2xl rounded-bl-none border border-slate-200 shadow-sm flex items-center space-x-2">
                <div className="w-2 h-2 bg-indigo-400 rounded-full animate-bounce" style={{ animationDelay: '0ms' }} />
                <div className="w-2 h-2 bg-indigo-400 rounded-full animate-bounce" style={{ animationDelay: '150ms' }} />
                <div className="w-2 h-2 bg-indigo-400 rounded-full animate-bounce" style={{ animationDelay: '300ms' }} />
              </div>
            </div>
          )}
          <div ref={messagesEndRef} />
        </div>

        {/* Chat Input */}
        <div className="p-4 bg-white border-t border-slate-200">
          <div className="flex items-center space-x-2">
            <input
              type="text"
              value={input}
              onChange={(e) => setInput(e.target.value)}
              onKeyDown={(e) => e.key === 'Enter' && handleSend()}
              placeholder="Kérdezz valamit..."
              className="flex-1 border border-slate-300 rounded-xl px-4 py-3 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:border-transparent"
            />
            <button 
              onClick={handleSend}
              disabled={!input.trim()}
              className="bg-indigo-600 text-white p-3 rounded-xl hover:bg-indigo-700 disabled:opacity-50 disabled:cursor-not-allowed transition-colors"
            >
              <Send className="w-5 h-5" />
            </button>
          </div>
        </div>
      </div>
    </div>
  );
}

// --- Komponens: Dokumentum Elemző Modul ---
function DocumentAnalysisModule() {
  const [file, setFile] = useState(null);
  const [isAnalyzing, setIsAnalyzing] = useState(false);
  const [result, setResult] = useState(null);

  const handleFileUpload = (e) => {
    const uploadedFile = e.target.files[0];
    if (uploadedFile) {
      setFile(uploadedFile);
      setResult(null);
    }
  };

  const startAnalysis = () => {
    if (!file) return;
    setIsAnalyzing(true);
    
    setTimeout(() => {
      setIsAnalyzing(false);
      setResult(simulateDocAnalysis());
    }, 3000);
  };

  const reset = () => {
    setFile(null);
    setResult(null);
  };

  return (
    <div className="max-w-5xl mx-auto px-4 py-12">
      <div className="text-center mb-10">
        <h2 className="text-3xl font-bold text-slate-900 mb-3">Dokumentum Elemző</h2>
        <p className="text-slate-600 max-w-2xl mx-auto">
          Tölts fel egy hosszú, bonyolult PDF-et vagy szöveges fájlt, és az AI kiemeli a lényeget egyszerű, érthető pontokban.
        </p>
      </div>

      <div className="grid grid-cols-1 md:grid-cols-2 gap-8 items-start">
        
        {/* Bal oldal: Feltöltés */}
        <div className="bg-white rounded-xl shadow-sm border border-slate-200 p-8 h-full">
          <h3 className="text-lg font-semibold mb-6 flex items-center">
            <div className="bg-indigo-100 p-2 rounded-lg mr-3">
              <Upload className="w-5 h-5 text-indigo-600" />
            </div>
            Fájl feltöltése
          </h3>
          
          {!file ? (
            <div className="border-2 border-dashed border-slate-300 rounded-xl p-10 text-center hover:bg-slate-50 transition-colors relative cursor-pointer">
               <input 
                type="file" 
                className="absolute inset-0 w-full h-full opacity-0 cursor-pointer"
                onChange={handleFileUpload}
                accept=".txt,.pdf,.doc,.docx"
              />
              <div className="flex justify-center mb-4">
                <FileText className="w-12 h-12 text-slate-400" />
              </div>
              <p className="text-slate-900 font-medium">Húzd ide a fájlt, vagy kattints</p>
              <p className="text-slate-500 text-sm mt-2">Támogatott formátumok: PDF, DOCX, TXT</p>
            </div>
          ) : (
            <div className="bg-indigo-50 border border-indigo-100 rounded-xl p-6 text-center">
              <div className="flex items-center justify-center mb-4 bg-white w-16 h-16 rounded-full shadow-sm mx-auto">
                <CheckCircle className="w-8 h-8 text-green-500" />
              </div>
              <p className="font-semibold text-indigo-900 truncate max-w-xs mx-auto">{file.name}</p>
              <p className="text-indigo-600 text-sm mb-6">{(file.size / 1024).toFixed(2)} KB</p>
              
              {!isAnalyzing && !result && (
                <div className="flex flex-col gap-3">
                  <button 
                    onClick={startAnalysis}
                    className="w-full py-3 bg-indigo-600 text-white rounded-lg font-medium hover:bg-indigo-700 transition-colors flex items-center justify-center"
                  >
                    <Cpu className="w-4 h-4 mr-2" />
                    Elemzés Indítása
                  </button>
                  <button 
                    onClick={reset}
                    className="w-full py-2 text-slate-500 hover:text-slate-700 text-sm"
                  >
                    Másik fájl választása
                  </button>
                </div>
              )}

              {isAnalyzing && (
                <div className="mt-4">
                  <div className="w-full bg-indigo-200 rounded-full h-2.5 mb-2">
                    <div className="bg-indigo-600 h-2.5 rounded-full animate-pulse w-3/4"></div>
                  </div>
                  <p className="text-sm text-indigo-700 animate-pulse">A dokumentum feldolgozása...</p>
                </div>
              )}
            </div>
          )}
        </div>

        {/* Jobb oldal: Eredmény */}
        <div className={`bg-white rounded-xl shadow-sm border border-slate-200 p-8 h-full min-h-[400px] relative transition-all duration-500 ${result ? 'opacity-100' : 'opacity-70'}`}>
           <h3 className="text-lg font-semibold mb-6 flex items-center">
            <div className="bg-green-100 p-2 rounded-lg mr-3">
              <Brain className="w-5 h-5 text-green-600" />
            </div>
            Elemzés Eredménye
          </h3>

          {!result && !isAnalyzing && (
            <div className="flex flex-col items-center justify-center h-64 text-slate-400">
              <Cpu className="w-16 h-16 mb-4 opacity-20" />
              <p>Az eredmények itt fognak megjelenni</p>
            </div>
          )}

          {isAnalyzing && (
            <div className="flex flex-col items-center justify-center h-64 text-indigo-600">
              <div className="animate-spin rounded-full h-12 w-12 border-b-2 border-indigo-600 mb-4"></div>
              <p>AI gondolkodik...</p>
            </div>
          )}

          {result && (
            <div className="animate-fadeIn">
              <div className="prose prose-indigo text-slate-700 bg-slate-50 p-6 rounded-lg border border-slate-100 text-sm sm:text-base whitespace-pre-line">
                {result}
              </div>
              <div className="mt-6 flex justify-between items-center border-t border-slate-100 pt-4">
                <span className="text-xs text-slate-500">Generálva: {new Date().toLocaleTimeString()}</span>
                <button className="text-indigo-600 hover:text-indigo-800 text-sm font-medium flex items-center">
                  Másolás vágólapra <ChevronRight className="w-4 h-4 ml-1" />
                </button>
              </div>
               <button 
                  onClick={reset}
                  className="mt-4 w-full py-2 border border-slate-200 text-slate-600 rounded-lg hover:bg-slate-50 transition-colors text-sm md:hidden"
                >
                  Új elemzés
                </button>
            </div>
          )}
        </div>
      </div>
    </div>
  );
}

// --- Komponens: Média Generátor Modul (ÚJ) ---
function MediaGeneratorModule() {
  const [mediaType, setMediaType] = useState('image'); // 'image' vagy 'video'
  const [prompt, setPrompt] = useState('');
  const [isGenerating, setIsGenerating] = useState(false);
  const [generatedMedia, setGeneratedMedia] = useState(null);

  const handleGenerate = () => {
    if (!prompt.trim()) return;
    setIsGenerating(true);
    setGeneratedMedia(null);

    // Szimulált generálási idő
    setTimeout(() => {
      setIsGenerating(false);
      // Minta tartalom generálása a prompt alapján (mock)
      if (mediaType === 'image') {
        // Picsum fotó használata a változatosság kedvéért, seed-ként a prompttal
        setGeneratedMedia(`https://picsum.photos/seed/${encodeURIComponent(prompt)}/800/600`);
      } else {
        // Videó placeholder
        setGeneratedMedia('mock_video');
      }
    }, 2500);
  };

  return (
    <div className="max-w-4xl mx-auto px-4 py-12">
      <div className="text-center mb-10">
        <h2 className="text-3xl font-bold text-slate-900 mb-3">Média Stúdió</h2>
        <p className="text-slate-600 max-w-2xl mx-auto">
          Írd le, mit szeretnél látni, és az AI létrehozza neked. Válassz kép vagy videó generálás között.
        </p>
      </div>

      <div className="bg-white rounded-2xl shadow-lg border border-slate-200 overflow-hidden">
        {/* Vezérlőpult */}
        <div className="p-6 sm:p-8 border-b border-slate-100 bg-slate-50">
          
          {/* Típus választó fülek */}
          <div className="flex justify-center mb-8">
            <div className="bg-white p-1 rounded-xl border border-slate-200 inline-flex shadow-sm">
              <button
                onClick={() => { setMediaType('image'); setGeneratedMedia(null); }}
                className={`flex items-center px-6 py-2.5 rounded-lg text-sm font-semibold transition-all ${
                  mediaType === 'image' 
                    ? 'bg-indigo-600 text-white shadow-md' 
                    : 'text-slate-600 hover:bg-slate-50'
                }`}
              >
                <ImageIcon className="w-4 h-4 mr-2" />
                Kép Generálás
              </button>
              <button
                onClick={() => { setMediaType('video'); setGeneratedMedia(null); }}
                className={`flex items-center px-6 py-2.5 rounded-lg text-sm font-semibold transition-all ${
                  mediaType === 'video' 
                    ? 'bg-indigo-600 text-white shadow-md' 
                    : 'text-slate-600 hover:bg-slate-50'
                }`}
              >
                <Video className="w-4 h-4 mr-2" />
                Videó Generálás
              </button>
            </div>
          </div>

          {/* Input Mező */}
          <div className="max-w-2xl mx-auto">
            <div className="relative">
              <textarea
                value={prompt}
                onChange={(e) => setPrompt(e.target.value)}
                placeholder={mediaType === 'image' ? "Pl.: Egy futurisztikus város lebegő autókkal naplementében..." : "Pl.: Egy drónfelvétel ahogy hullámok csapódnak a sziklákhoz lassítva..."}
                className="w-full border border-slate-300 rounded-xl px-4 py-4 pb-12 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:border-transparent min-h-[120px] resize-none shadow-sm"
              />
              <div className="absolute bottom-3 right-3">
                <button
                  onClick={handleGenerate}
                  disabled={!prompt.trim() || isGenerating}
                  className="bg-indigo-600 text-white px-4 py-2 rounded-lg font-medium text-sm hover:bg-indigo-700 disabled:opacity-50 disabled:cursor-not-allowed transition-colors flex items-center"
                >
                  {isGenerating ? (
                    <>
                      <div className="animate-spin rounded-full h-4 w-4 border-2 border-white border-t-transparent mr-2"></div>
                      Alkotás...
                    </>
                  ) : (
                    <>
                      <Wand2 className="w-4 h-4 mr-2
