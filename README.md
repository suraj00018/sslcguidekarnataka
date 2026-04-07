import React, { useState, useEffect } from 'react';
import { 
  BookOpen, Microscope, Calculator, Globe, Type, Sun, Moon, 
  Search, Menu, X, ChevronRight, PlayCircle, CheckCircle, 
  AlertCircle, FileText, HelpCircle, Award, Clock, Lock, Edit, Plus, Save, Trash2, Database,
  ArrowRight, Sparkles, BookMarked, Target, Image as ImageIcon, LayoutDashboard, Home
} from 'lucide-react';

// --- INITIAL DATA STATE ---
const initialData = {
  homePage: {
    heroBadge: "Karnataka's #1 Learning Platform",
    heroTitleLine1: "Score 95%+ in",
    heroTitleLine2: "SSLC Board Exams",
    heroSubtitle: "Bilingual notes, chapter-wise mock tests, and smart revision materials. Designed to make learning effortless.",
    updates: [
      "Model Question Papers 2026 released by KSEAB.",
      "Science Chapter 5 Notes updated with high-res diagrams.",
      "New 1-mark MCQ speed quiz added for Mathematics."
    ]
  },
  subjects: [
    { id: 'science', name: 'Science (ವಿಜ್ಞಾನ)', iconName: 'microscope', color: 'blue' },
    { id: 'math', name: 'Mathematics (ಗಣಿತ)', iconName: 'calculator', color: 'red' },
    { id: 'social', name: 'Social Science (ಸಮಾಜ ವಿಜ್ಞಾನ)', iconName: 'globe', color: 'emerald' },
    { id: 'english', name: 'English (ಇಂಗ್ಲಿಷ್)', iconName: 'type', color: 'purple' },
    { id: 'kannada', name: 'Kannada (ಕನ್ನಡ)', iconName: 'book', color: 'amber' },
    { id: 'hindi', name: 'Hindi (हिंदी)', iconName: 'filetext', color: 'orange' },
  ],
  chapters: {
    science: [
      { id: 'sci_ch1', name: '1. Chemical Reactions and Equations', kannadaName: 'ರಾಸಾಯನಿಕ ಕ್ರಿಯೆಗಳು ಮತ್ತು ಸಮೀಕರಣಗಳು', weightage: '5 Marks' }
    ],
    social: [], math: [], english: [], kannada: [], hindi: []
  },
  chapterContent: {
    'sci_ch1': {
      english: {
        notes: [
          {
            title: "What is a Chemical Reaction?",
            content: "A process in which new substances with new properties are formed.",
            example: "Example: Digestion of food, Rusting of iron.",
            imageUrls: [],
            pdfLinks: []
          },
          {
            title: "Chemical Equation",
            content: "Representing a chemical reaction using symbols and formulas.",
            example: "Mg + O2 → MgO",
            imageUrls: ["https://upload.wikimedia.org/wikipedia/commons/thumb/e/e0/Magnesium_ribbon_burning.jpg/320px-Magnesium_ribbon_burning.jpg"],
            pdfLinks: ["https://drive.google.com/example-link"]
          }
        ],
        summary: "In this chapter, we learned how to write and balance chemical equations.",
        questions: {
          marks1: [{ q: "Why should a magnesium ribbon be cleaned?", a: "To remove the protective layer." }],
          marks2: [], marks3: [], marks5: []
        },
        mcqs: [
          {
            question: "Which of the following is a physical change?",
            options: ["Rusting of iron", "Combustion of Magnesium", "Melting of ice", "Burning of paper"],
            correct: 2
          }
        ]
      },
      kannada: {
        notes: [
          {
            title: "ರಾಸಾಯನಿಕ ಕ್ರಿಯೆ ಎಂದರೇನು?",
            content: "ಹೊಸ ಗುಣಲಕ್ಷಣಗಳನ್ನು ಹೊಂದಿರುವ ಹೊಸ ವಸ್ತುಗಳು ಉತ್ಪತ್ತಿಯಾಗುವ ಪ್ರಕ್ರಿಯೆ.",
            example: "ಉದಾಹರಣೆ: ಆಹಾರದ ಜೀರ್ಣಕ್ರಿಯೆ, ಕಬ್ಬಿಣದ ತುಕ್ಕು.",
            imageUrls: [],
            pdfLinks: []
          },
          {
            title: "ರಾಸಾಯನಿಕ ಸಮೀಕರಣ",
            content: "ಸಂಕೇತಗಳು ಮತ್ತು ಸೂತ್ರಗಳನ್ನು ಬಳಸಿ ರಾಸಾಯನಿಕ ಕ್ರಿಯೆಯನ್ನು ಪ್ರತಿನಿಧಿಸುವುದು.",
            example: "Mg + O2 → MgO",
            imageUrls: ["https://upload.wikimedia.org/wikipedia/commons/thumb/e/e0/Magnesium_ribbon_burning.jpg/320px-Magnesium_ribbon_burning.jpg"],
            pdfLinks: []
          }
        ],
        summary: "ಈ ಅಧ್ಯಾಯದಲ್ಲಿ, ರಾಸಾಯನಿಕ ಸಮೀಕರಣಗಳನ್ನು ಹೇಗೆ ಬರೆಯುವುದು ಮತ್ತು ಸಮತೋಲನಗೊಳಿಸುವುದು ಎಂಬುದನ್ನು ನಾವು ಕಲಿತಿದ್ದೇವೆ.",
        questions: {
          marks1: [{ q: "ಮೆಗ್ನೀಸಿಯಮ್ ರಿಬ್ಬನ್ ಅನ್ನು ಏಕೆ ಸ್ವಚ್ಛಗೊಳಿಸಬೇಕು?", a: "ರಕ್ಷಣಾತ್ಮಕ ಪದರವನ್ನು ತೆಗೆದುಹಾಕಲು." }],
          marks2: [], marks3: [], marks5: []
        },
        mcqs: [
          {
            question: "ಕೆಳಗಿನವುಗಳಲ್ಲಿ ಯಾವುದು ಭೌತಿಕ ಬದಲಾವಣೆಯಾಗಿದೆ?",
            options: ["ಕಬ್ಬಿಣದ ತುಕ್ಕು", "ಮೆಗ್ನೀಸಿಯಮ್ ದಹನ", "ಮಂಜುಗಡ್ಡೆಯ ಕರಗುವಿಕೆ", "ಕಾಗದದ ಸುಡುವಿಕೆ"],
            correct: 2
          }
        ]
      }
    }
  },
  pyqs: [
    { id: 'pyq_1', year: '2025', title: 'Science Model Question Paper (KSEAB)', link: '#' },
    { id: 'pyq_2', year: '2024', title: 'Mathematics Final Board Paper', link: '#' }
  ]
};

const getSubjectIcon = (iconName, className) => {
  switch(iconName) {
    case 'microscope': return <Microscope className={className} />;
    case 'calculator': return <Calculator className={className} />;
    case 'globe': return <Globe className={className} />;
    case 'type': return <Type className={className} />;
    case 'filetext': return <FileText className={className} />;
    case 'book': 
    default: return <BookOpen className={className} />;
  }
};

const colorMap = {
  blue: { bg: 'bg-blue-50 dark:bg-blue-900/20', text: 'text-blue-600 dark:text-blue-400', border: 'border-blue-200 dark:border-blue-800/50', gradient: 'from-blue-500 to-cyan-500' },
  red: { bg: 'bg-red-50 dark:bg-red-900/20', text: 'text-red-600 dark:text-red-400', border: 'border-red-200 dark:border-red-800/50', gradient: 'from-red-500 to-pink-500' },
  emerald: { bg: 'bg-emerald-50 dark:bg-emerald-900/20', text: 'text-emerald-600 dark:text-emerald-400', border: 'border-emerald-200 dark:border-emerald-800/50', gradient: 'from-emerald-500 to-teal-500' },
  purple: { bg: 'bg-purple-50 dark:bg-purple-900/20', text: 'text-purple-600 dark:text-purple-400', border: 'border-purple-200 dark:border-purple-800/50', gradient: 'from-purple-500 to-indigo-500' },
  amber: { bg: 'bg-amber-50 dark:bg-amber-900/20', text: 'text-amber-600 dark:text-amber-400', border: 'border-amber-200 dark:border-amber-800/50', gradient: 'from-amber-500 to-orange-500' },
  orange: { bg: 'bg-orange-50 dark:bg-orange-900/20', text: 'text-orange-600 dark:text-orange-400', border: 'border-orange-200 dark:border-orange-800/50', gradient: 'from-orange-500 to-red-500' },
};

// --- COMPONENTS ---

const SEOHandler = ({ title }) => {
  useEffect(() => {
    document.title = `${title} | Karnataka SSLC Prep Hub`;
  }, [title]);
  return null;
};

export default function App() {
  const [currentView, setCurrentView] = useState('home');
  const [darkMode, setDarkMode] = useState(false);
  const [menuOpen, setMenuOpen] = useState(false);
  const [searchQuery, setSearchQuery] = useState('');

  // App UI States (Custom Alerts/Modals replacing window.alert)
  const [toastMsg, setToastMsg] = useState('');
  const [confirmDialog, setConfirmDialog] = useState(null);

  const showToast = (msg) => {
    setToastMsg(msg);
    setTimeout(() => setToastMsg(''), 3000);
  };

  // Admin & Global State
  const [appData, setAppData] = useState(initialData);
  const [isAdmin, setIsAdmin] = useState(false);
  const [activeSubject, setActiveSubject] = useState(null);
  const [activeChapter, setActiveChapter] = useState(null);
  const [studyMedium, setStudyMedium] = useState('english');

  useEffect(() => {
    if (darkMode) document.documentElement.classList.add('dark');
    else document.documentElement.classList.remove('dark');
  }, [darkMode]);

  const navigateTo = (view, subjectId = null, chapterId = null) => {
    if (subjectId) setActiveSubject(subjectId);
    if (chapterId) setActiveChapter(chapterId);
    setCurrentView(view);
    setMenuOpen(false);
    window.scrollTo(0, 0);
  };

  return (
    <div className="min-h-screen bg-[#F8FAFC] dark:bg-[#0B1120] text-slate-900 dark:text-slate-100 font-sans transition-colors duration-300 selection:bg-indigo-500/30 relative">
      
      {/* CUSTOM TOAST NOTIFICATION */}
      {toastMsg && (
        <div className="fixed bottom-6 right-6 bg-slate-900 dark:bg-white text-white dark:text-slate-900 px-6 py-4 rounded-2xl shadow-2xl z-[100] animate-fade-in flex items-center font-bold">
          <CheckCircle className="w-5 h-5 mr-3 text-emerald-400 dark:text-emerald-500" />
          {toastMsg}
        </div>
      )}

      {/* CUSTOM CONFIRM DIALOG */}
      {confirmDialog && (
        <div className="fixed inset-0 bg-slate-900/40 backdrop-blur-sm z-[100] flex items-center justify-center p-4">
          <div className="bg-white dark:bg-slate-800 p-8 rounded-[2rem] shadow-2xl max-w-sm w-full animate-fade-in border border-slate-200 dark:border-slate-700">
            <div className="w-16 h-16 bg-red-50 dark:bg-red-900/30 text-red-500 rounded-full flex items-center justify-center mx-auto mb-4">
              <AlertCircle className="w-8 h-8" />
            </div>
            <h3 className="text-xl font-black text-center mb-8 text-slate-900 dark:text-white leading-snug">{confirmDialog.message}</h3>
            <div className="flex gap-4">
              <button onClick={() => setConfirmDialog(null)} className="flex-1 bg-slate-100 dark:bg-slate-700 text-slate-700 dark:text-slate-300 py-3 rounded-xl font-bold hover:bg-slate-200 dark:hover:bg-slate-600 transition">Cancel</button>
              <button onClick={() => { confirmDialog.onConfirm(); setConfirmDialog(null); }} className="flex-1 bg-red-500 hover:bg-red-600 text-white py-3 rounded-xl font-bold transition shadow-lg shadow-red-500/30">Confirm</button>
            </div>
          </div>
        </div>
      )}

      {/* STICKY NAVBAR */}
      <nav className="sticky top-0 z-50 bg-white/80 dark:bg-[#0B1120]/80 backdrop-blur-xl border-b border-slate-200/50 dark:border-slate-800/50">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="flex justify-between h-[4.5rem]">
            <div className="flex items-center cursor-pointer group" onClick={() => navigateTo('home')}>
              <div className="bg-gradient-to-tr from-indigo-600 to-blue-500 p-2 rounded-xl mr-3 shadow-lg shadow-indigo-500/20 group-hover:scale-105 transition-transform">
                <Award className="w-6 h-6 text-white" />
              </div>
              <span className="font-extrabold text-xl tracking-tight text-slate-800 dark:text-white">
                SSLC<span className="text-transparent bg-clip-text bg-gradient-to-r from-indigo-600 to-blue-500 font-black">Hub.</span>
              </span>
            </div>
            
            {/* Desktop Menu */}
            <div className="hidden md:flex items-center space-x-2">
              <div className="relative mr-4">
                <input 
                  type="text" 
                  placeholder="Search..." 
                  value={searchQuery}
                  onChange={(e) => setSearchQuery(e.target.value)}
                  className="bg-slate-100/80 dark:bg-slate-800/80 rounded-full px-5 py-2 pl-11 focus:outline-none focus:ring-2 focus:ring-indigo-500 text-sm w-64 transition-all border border-transparent dark:border-slate-700"
                />
                <Search className="w-4 h-4 absolute left-4 top-2.5 text-slate-400" />
              </div>
              <button onClick={() => navigateTo('home')} className="px-4 py-2 rounded-full text-sm font-semibold hover:bg-slate-100 dark:hover:bg-slate-800 transition-colors">Home</button>
              <button onClick={() => navigateTo('revision')} className="px-4 py-2 rounded-full text-sm font-semibold hover:bg-slate-100 dark:hover:bg-slate-800 transition-colors">Revision</button>
              <button onClick={() => navigateTo('pyq')} className="px-4 py-2 rounded-full text-sm font-semibold hover:bg-slate-100 dark:hover:bg-slate-800 transition-colors">PYQs</button>
              <div className="h-6 w-px bg-slate-200 dark:bg-slate-800 mx-2"></div>
              <button 
                onClick={() => setDarkMode(!darkMode)}
                className="p-2.5 rounded-full hover:bg-slate-100 dark:hover:bg-slate-800 transition-colors"
              >
                {darkMode ? <Sun className="w-5 h-5 text-amber-400" /> : <Moon className="w-5 h-5 text-slate-600" />}
              </button>
            </div>

            {/* Mobile Menu Button */}
            <div className="md:hidden flex items-center">
              <button onClick={() => setDarkMode(!darkMode)} className="p-2 mr-2 rounded-full hover:bg-slate-100 dark:hover:bg-slate-800 transition">
                {darkMode ? <Sun className="w-5 h-5 text-amber-400" /> : <Moon className="w-5 h-5" />}
              </button>
              <button onClick={() => setMenuOpen(!menuOpen)} className="p-2 rounded-full hover:bg-slate-100 dark:hover:bg-slate-800">
                {menuOpen ? <X className="w-6 h-6" /> : <Menu className="w-6 h-6" />}
              </button>
            </div>
          </div>
        </div>

        {/* Mobile Menu Dropdown */}
        {menuOpen && (
          <div className="md:hidden bg-white/95 dark:bg-[#0B1120]/95 backdrop-blur-xl border-b border-slate-200 dark:border-slate-800 absolute w-full left-0 shadow-xl">
            <div className="px-4 pt-4 pb-6 space-y-2">
              <button onClick={() => navigateTo('home')} className="block w-full text-left px-4 py-3 rounded-xl font-semibold hover:bg-slate-100 dark:hover:bg-slate-800">Home</button>
              <button onClick={() => navigateTo('revision')} className="block w-full text-left px-4 py-3 rounded-xl font-semibold hover:bg-slate-100 dark:hover:bg-slate-800">Last Minute Revision</button>
              <button onClick={() => navigateTo('pyq')} className="block w-full text-left px-4 py-3 rounded-xl font-semibold hover:bg-slate-100 dark:hover:bg-slate-800">Previous Papers</button>
              {isAdmin && <button onClick={() => navigateTo('admin_dashboard')} className="block w-full text-left px-4 py-3 rounded-xl font-semibold text-indigo-500 hover:bg-indigo-50 dark:hover:bg-indigo-900/20 mt-4">⚙️ Admin Panel</button>}
            </div>
          </div>
        )}
      </nav>

      {/* MAIN CONTENT AREA */}
      <main className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-10 lg:py-12">
        {currentView === 'home' && <HomePage navigateTo={navigateTo} appData={appData} showToast={showToast} />}
        {currentView === 'subject_view' && <SubjectPage navigateTo={navigateTo} appData={appData} subjectId={activeSubject} showToast={showToast} studyMedium={studyMedium} setStudyMedium={setStudyMedium} />}
        {currentView === 'chapter_view' && <ChapterPage navigateTo={navigateTo} appData={appData} subjectId={activeSubject} chapterId={activeChapter} studyMedium={studyMedium} setStudyMedium={setStudyMedium} />}
        {currentView === 'pyq' && <PyqPage navigateTo={navigateTo} appData={appData} />}
        {currentView === 'revision' && <RevisionPage navigateTo={navigateTo} appData={appData} />}
        {currentView === 'admin_login' && <AdminLogin navigateTo={navigateTo} setIsAdmin={setIsAdmin} showToast={showToast} />}
        {currentView === 'admin_dashboard' && <AdminDashboard navigateTo={navigateTo} appData={appData} setAppData={setAppData} isAdmin={isAdmin} showToast={showToast} setConfirmDialog={setConfirmDialog} />}
      </main>

      {/* FOOTER */}
      <footer className="bg-white dark:bg-[#0B1120] border-t border-slate-200 dark:border-slate-800 mt-20 pt-16 pb-8">
        <div className="max-w-7xl mx-auto px-4 text-center">
          <p className="text-slate-800 dark:text-slate-200 font-bold text-lg mb-2">Karnataka SSLC Prep Hub</p>
          <div className="mt-8 pt-8 border-t border-slate-100 dark:border-slate-800/50 flex flex-col md:flex-row items-center justify-center">
            <p className="text-xs text-slate-400 mb-4 md:mb-0">
              <span onClick={() => navigateTo(isAdmin ? 'admin_dashboard' : 'admin_login')} className="cursor-default select-none">© 2026</span> EduPrep Hub. Not affiliated with KSEAB.
            </p>
          </div>
        </div>
      </footer>
    </div>
  );
}

// --- NEW PAGES (PYQ & Revision) ---
function PyqPage({ navigateTo, appData }) {
  const pyqs = appData.pyqs || [];

  return (
    <div className="animate-fade-in py-10">
      <SEOHandler title="Previous Papers" />
      <div className="text-center mb-12">
        <FileText className="w-16 h-16 mx-auto text-indigo-500 mb-6" />
        <h2 className="text-4xl font-black mb-4">Previous Year Question Papers</h2>
        <p className="text-slate-500 mb-8 max-w-lg mx-auto">Access board papers to practice actual exam patterns. Click to view or download.</p>
      </div>

      {pyqs.length === 0 ? (
        <div className="text-center py-20 bg-white dark:bg-slate-800 rounded-[2.5rem] shadow-sm border border-slate-100 dark:border-slate-700">
          <p className="text-slate-500 font-medium">Content uploading soon...</p>
          <button onClick={() => navigateTo('home')} className="mt-6 bg-slate-900 dark:bg-white text-white dark:text-slate-900 font-bold py-3 px-8 rounded-full">Return Home</button>
        </div>
      ) : (
        <div className="grid md:grid-cols-2 lg:grid-cols-3 gap-6 max-w-6xl mx-auto">
          {pyqs.map(pyq => (
            <a key={pyq.id} href={pyq.link} target="_blank" rel="noreferrer" className="bg-white dark:bg-slate-800 p-6 rounded-2xl border border-slate-200 dark:border-slate-700 shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all flex flex-col justify-between group h-full">
              <div className="flex items-start gap-4 mb-4">
                <div className="w-12 h-12 rounded-xl bg-indigo-50 dark:bg-indigo-900/30 flex items-center justify-center text-indigo-600 dark:text-indigo-400 shrink-0 group-hover:scale-110 transition-transform">
                  <FileText className="w-6 h-6" />
                </div>
                <div>
                  <div className="text-xs font-bold text-indigo-500 mb-1 bg-indigo-50 dark:bg-indigo-900/30 inline-block px-2 py-0.5 rounded uppercase tracking-wider">{pyq.year}</div>
                  <h3 className="font-bold text-slate-900 dark:text-white leading-snug group-hover:text-indigo-600 dark:group-hover:text-indigo-400 transition-colors">{pyq.title}</h3>
                </div>
              </div>
              <div className="text-sm font-bold text-slate-400 group-hover:text-indigo-500 flex items-center mt-2">
                View Paper <ArrowRight className="w-4 h-4 ml-1" />
              </div>
            </a>
          ))}
        </div>
      )}
    </div>
  );
}

function RevisionPage({ navigateTo, appData }) {
  return (
    <div className="animate-fade-in text-center py-20 bg-white dark:bg-slate-800 rounded-[2.5rem] shadow-sm border border-slate-100 dark:border-slate-700">
      <SEOHandler title="Revision" />
      <Clock className="w-20 h-20 mx-auto text-amber-300 dark:text-amber-700 mb-6" />
      <h2 className="text-3xl font-black mb-4">Last Minute Revision Hub</h2>
      <p className="text-slate-500 mb-8 max-w-lg mx-auto">Quick summaries, mind maps, and vital formulas across all subjects to brush up the day before the exam.</p>
      <div className="flex justify-center flex-wrap gap-4 max-w-2xl mx-auto">
        {appData.subjects.map(sub => (
          <button key={sub.id} onClick={() => navigateTo('subject_view', sub.id)} className="px-6 py-3 rounded-full border-2 border-slate-200 dark:border-slate-700 font-bold hover:border-indigo-500 hover:text-indigo-500 transition-colors">
            {sub.name.split(' ')[0]} Hub
          </button>
        ))}
      </div>
    </div>
  );
}


// --- HOME PAGE COMPONENT ---
function HomePage({ navigateTo, appData, showToast }) {
  const hp = appData.homePage;

  return (
    <div className="space-y-16 animate-fade-in">
      <SEOHandler title="Home" />

      {/* Modern Hero Section - Driven by Admin State */}
      <section className="relative text-center py-20 px-4 rounded-[2.5rem] bg-white dark:bg-[#111827] shadow-xl shadow-slate-200/40 dark:shadow-none border border-slate-100 dark:border-slate-800 overflow-hidden isolate">
        <div className="absolute top-0 left-1/2 -translate-x-1/2 w-full h-full max-w-3xl overflow-hidden -z-10 pointer-events-none opacity-40 dark:opacity-20">
          <div className="absolute -top-24 -left-24 w-96 h-96 bg-blue-400 rounded-full mix-blend-multiply filter blur-3xl opacity-70"></div>
          <div className="absolute top-12 -right-24 w-96 h-96 bg-purple-400 rounded-full mix-blend-multiply filter blur-3xl opacity-70"></div>
        </div>

        {hp.heroBadge && (
          <div className="inline-flex items-center px-4 py-2 rounded-full bg-indigo-50 dark:bg-indigo-900/30 text-indigo-600 dark:text-indigo-300 text-sm font-bold mb-8 border border-indigo-100 dark:border-indigo-800/50 shadow-sm">
            <Sparkles className="w-4 h-4 mr-2" /> {hp.heroBadge}
          </div>
        )}
        
        <h1 className="text-5xl md:text-6xl lg:text-7xl font-black tracking-tight mb-6 text-slate-900 dark:text-white">
          {hp.heroTitleLine1} <br className="hidden sm:block" />
          <span className="text-transparent bg-clip-text bg-gradient-to-r from-indigo-600 to-blue-500 dark:from-indigo-400 dark:to-blue-400">{hp.heroTitleLine2}</span>
        </h1>
        
        <p className="text-lg md:text-xl text-slate-600 dark:text-slate-300 mb-10 max-w-2xl mx-auto leading-relaxed whitespace-pre-line">
          {hp.heroSubtitle}
        </p>
        
        <div className="flex flex-col sm:flex-row justify-center gap-4 sm:gap-6">
          <button onClick={() => navigateTo('revision')} className="bg-slate-900 dark:bg-white text-white dark:text-slate-900 font-bold py-4 px-8 rounded-full transition-all duration-300 shadow-xl hover:-translate-y-1 flex items-center justify-center text-lg">
            <Clock className="w-5 h-5 mr-2" /> Start Revision Now
          </button>
          <button onClick={() => navigateTo('pyq')} className="bg-white dark:bg-slate-800 hover:bg-slate-50 dark:hover:bg-slate-700 text-slate-700 dark:text-slate-200 font-bold py-4 px-8 rounded-full transition-all duration-300 shadow-sm border border-slate-200 dark:border-slate-700 flex items-center justify-center text-lg hover:-translate-y-1">
            <FileText className="w-5 h-5 mr-2" /> View Previous Papers
          </button>
        </div>
      </section>

      {/* Subjects Grid */}
      <section>
        <div className="flex items-center justify-between mb-8">
          <h2 className="text-3xl font-black text-slate-900 dark:text-white flex items-center">
            <BookMarked className="w-7 h-7 mr-3 text-indigo-500" /> Explore Subjects
          </h2>
        </div>
        <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6 lg:gap-8">
          {appData.subjects.map((sub) => {
            const theme = colorMap[sub.color] || colorMap['blue'];
            return (
              <div 
                key={sub.id}
                onClick={() => {
                  if (appData.chapters[sub.id] && appData.chapters[sub.id].length > 0) {
                    navigateTo('subject_view', sub.id);
                  } else {
                    showToast('Content uploading soon! Check back later.');
                  }
                }}
                className={`group bg-white dark:bg-slate-800 p-8 rounded-[2rem] shadow-sm hover:shadow-2xl hover:-translate-y-1 transition-all duration-300 cursor-pointer border border-slate-100 dark:border-slate-700 relative overflow-hidden`}
              >
                <div className={`absolute top-0 left-0 w-full h-1.5 bg-gradient-to-r ${theme.gradient} opacity-0 group-hover:opacity-100 transition-opacity duration-300`}></div>
                
                <div className="flex items-center justify-between mb-6">
                  <div className={`p-4 rounded-2xl ${theme.bg} ${theme.text}`}>
                    {getSubjectIcon(sub.iconName, "w-8 h-8")}
                  </div>
                  <div className={`w-10 h-10 rounded-full flex items-center justify-center bg-slate-50 dark:bg-slate-700 group-hover:${theme.bg} transition-colors`}>
                    <ArrowRight className={`w-5 h-5 text-slate-400 group-hover:${theme.text} transition-colors`} />
                  </div>
                </div>
                <div>
                  <h3 className="text-2xl font-bold text-slate-900 dark:text-white mb-1">{sub.name.split(' ')[0]}</h3>
                  <p className="text-slate-500 dark:text-slate-400 font-medium">{sub.name.split(' ').slice(1).join(' ')}</p>
                </div>
                <div className="mt-6 inline-flex items-center px-3 py-1 rounded-lg bg-slate-50 dark:bg-slate-700/50 text-xs font-semibold text-slate-500 dark:text-slate-400 border border-slate-100 dark:border-slate-700">
                  {appData.chapters[sub.id]?.length || 0} Chapters
                </div>
              </div>
            );
          })}
        </div>
      </section>

      {/* Modern Info Cards */}
      <section className="grid md:grid-cols-2 gap-8">
        <div className="bg-amber-50 dark:bg-amber-900/10 p-10 rounded-[2.5rem] border border-amber-100 dark:border-amber-900/30 relative overflow-hidden">
          <div className="absolute -right-8 -top-8 w-32 h-32 bg-amber-200/50 dark:bg-amber-500/10 rounded-full blur-2xl"></div>
          <h3 className="text-2xl font-black flex items-center text-amber-900 dark:text-amber-400 mb-6 relative z-10">
            <AlertCircle className="w-7 h-7 mr-3" /> Latest Updates
          </h3>
          <ul className="space-y-4 relative z-10">
            {hp.updates.map((text, i) => (
              <li key={i} className="flex items-start bg-white/60 dark:bg-slate-800/60 p-3 rounded-xl backdrop-blur-sm shadow-sm border border-white/50 dark:border-slate-700/50">
                <CheckCircle className="w-5 h-5 text-amber-500 mr-3 shrink-0 mt-0.5" /> 
                <span className="text-slate-800 dark:text-slate-200 font-medium leading-snug">{text}</span>
              </li>
            ))}
            {hp.updates.length === 0 && <p className="text-sm text-slate-500 font-medium">No recent updates.</p>}
          </ul>
        </div>
        
        <div className="bg-gradient-to-br from-indigo-600 to-blue-600 p-10 rounded-[2.5rem] shadow-xl shadow-blue-500/20 text-white flex flex-col justify-center items-start relative overflow-hidden">
          <div className="absolute right-0 bottom-0 opacity-10">
            <Clock className="w-64 h-64 -mb-16 -mr-16" />
          </div>
          <div className="inline-block px-3 py-1 bg-white/20 rounded-full text-xs font-bold tracking-wider uppercase mb-4 backdrop-blur-md">Exam Prep</div>
          <h3 className="text-3xl sm:text-4xl font-black mb-4">Last Minute Revision</h3>
          <p className="text-blue-100 mb-8 text-lg max-w-sm">Quick summaries, mind maps, and vital formulas to brush up the day before the exam.</p>
          <button onClick={() => navigateTo('revision')} className="bg-white text-indigo-600 hover:bg-slate-50 font-black py-4 px-8 rounded-full inline-flex items-center transition-transform hover:scale-105 shadow-lg">
            Access Resources <ArrowRight className="w-5 h-5 ml-2" />
          </button>
        </div>
      </section>
    </div>
  );
}

// --- SUBJECT PAGE COMPONENT ---
function SubjectPage({ navigateTo, appData, subjectId, showToast, studyMedium, setStudyMedium }) {
  const subject = appData.subjects.find(s => s.id === subjectId);
  const chapters = appData.chapters[subjectId] || [];
  const theme = colorMap[subject?.color] || colorMap['blue'];

  return (
    <div className="animate-fade-in space-y-10">
      <SEOHandler title={subject?.name.split(' ')[0]} />

      <div>
        <div className="flex flex-col sm:flex-row sm:items-center justify-between mb-6 gap-4">
          <div className="flex items-center space-x-2 text-sm font-semibold text-slate-500 dark:text-slate-400">
            <button className="hover:text-indigo-500" onClick={() => navigateTo('home')}>Home</button>
            <ChevronRight className="w-4 h-4" /> 
            <span className="text-slate-900 dark:text-slate-100">{subject?.name.split(' ')[0]}</span>
          </div>
          
          {/* Study Medium Selection Toggle */}
          <div className="flex bg-slate-200/50 dark:bg-slate-800 p-1 rounded-xl w-fit border border-slate-200 dark:border-slate-700">
            <button 
              onClick={() => setStudyMedium('english')} 
              className={`px-4 py-2 rounded-lg text-sm font-bold transition-all ${studyMedium === 'english' ? 'bg-white dark:bg-slate-700 text-indigo-600 dark:text-indigo-400 shadow-sm' : 'text-slate-600 dark:text-slate-400 hover:bg-white/50 dark:hover:bg-slate-700/50'}`}
            >
              English Medium
            </button>
            <button 
              onClick={() => setStudyMedium('kannada')} 
              className={`px-4 py-2 rounded-lg text-sm font-bold transition-all ${studyMedium === 'kannada' ? 'bg-white dark:bg-slate-700 text-indigo-600 dark:text-indigo-400 shadow-sm' : 'text-slate-600 dark:text-slate-400 hover:bg-white/50 dark:hover:bg-slate-700/50'}`}
            >
              ಕನ್ನಡ ಮಾಧ್ಯಮ
            </button>
          </div>
        </div>
        
        <div className={`relative overflow-hidden bg-white dark:bg-slate-800 p-8 sm:p-12 rounded-[2.5rem] shadow-sm border border-slate-100 dark:border-slate-700 flex flex-col sm:flex-row items-center sm:items-start text-center sm:text-left gap-6`}>
          <div className={`absolute top-0 right-0 w-64 h-64 bg-gradient-to-bl ${theme.gradient} opacity-10 rounded-full blur-3xl -mr-20 -mt-20`}></div>
          <div className={`p-6 rounded-[2rem] shadow-inner ${theme.bg} ${theme.text} shrink-0`}>
            {getSubjectIcon(subject?.iconName, "w-16 h-16")}
          </div>
          <div className="z-10 mt-2">
            <h1 className="text-4xl sm:text-5xl font-black text-slate-900 dark:text-white mb-2">{subject?.name}</h1>
            <p className="text-lg text-slate-500 dark:text-slate-400 font-medium">Class 10 Board Syllabus</p>
          </div>
        </div>
      </div>

      <div>
        <h2 className="text-2xl font-black mb-6 flex items-center text-slate-900 dark:text-white">
          <BookOpen className="w-6 h-6 mr-3 text-slate-400" /> Course Modules
        </h2>
        
        <div className="grid gap-4">
          {chapters.map((ch, idx) => (
            <div 
              key={ch.id} 
              onClick={() => {
                if (appData.chapterContent[ch.id]) navigateTo('chapter_view', subjectId, ch.id);
                else showToast('Chapter content uploading soon!');
              }}
              className="group bg-white dark:bg-slate-800 p-6 rounded-2xl shadow-sm hover:shadow-md transition-all duration-200 flex flex-col sm:flex-row sm:items-center justify-between cursor-pointer border border-slate-200/60 dark:border-slate-700 hover:border-indigo-300 dark:hover:border-indigo-500/50"
            >
              <div className="flex items-start gap-4">
                <div className="hidden sm:flex mt-1 w-8 h-8 rounded-full bg-slate-100 dark:bg-slate-700 items-center justify-center text-slate-500 font-bold text-sm shrink-0">{idx + 1}</div>
                <div>
                  <h3 className="text-lg font-bold text-slate-900 dark:text-white group-hover:text-indigo-600 transition-colors">{ch.name}</h3>
                  <p className="text-sm text-slate-500 font-medium">{ch.kannadaName}</p>
                </div>
              </div>
              <div className="mt-4 sm:mt-0 flex items-center justify-between sm:justify-end w-full sm:w-auto gap-4">
                <span className={`px-3 py-1 rounded-full text-xs font-bold border ${theme.bg} ${theme.text} ${theme.border}`}>🎯 {ch.weightage}</span>
                <div className="w-10 h-10 rounded-full bg-slate-50 dark:bg-slate-700 flex items-center justify-center group-hover:bg-indigo-600 group-hover:text-white text-slate-400 transition-colors">
                  <ArrowRight className="w-5 h-5" />
                </div>
              </div>
            </div>
          ))}
        </div>
      </div>
    </div>
  );
}

// --- CHAPTER PAGE COMPONENT ---
function ChapterPage({ navigateTo, appData, subjectId, chapterId, studyMedium, setStudyMedium }) {
  const [activeTab, setActiveTab] = useState('notes');
  const subject = appData.subjects.find(s => s.id === subjectId);
  const chapterInfo = appData.chapters[subjectId]?.find(c => c.id === chapterId);
  
  // Extract content based on selected medium
  const baseContentData = appData.chapterContent[chapterId];
  // Fallback support for older data structs without dual-medium
  const chapterContentData = baseContentData && baseContentData.english ? baseContentData[studyMedium] : baseContentData;

  const theme = colorMap[subject?.color] || colorMap['blue'];

  if (!chapterContentData) return <div className="p-20 text-center font-bold text-xl">Content not found.</div>;

  return (
    <div className="animate-fade-in relative space-y-8">
      <div className="flex flex-col sm:flex-row sm:items-center justify-between gap-4">
        <div className="flex items-center space-x-2 text-sm font-semibold text-slate-500 dark:text-slate-400 flex-wrap gap-y-2">
          <button className="hover:text-indigo-500" onClick={() => navigateTo('home')}>Home</button>
          <ChevronRight className="w-4 h-4" /> 
          <button className="hover:text-indigo-500" onClick={() => navigateTo('subject_view', subjectId)}>{subject?.name.split(' ')[0]}</button>
          <ChevronRight className="w-4 h-4" /> 
          <span className="text-slate-900 dark:text-slate-100 py-1 px-3 bg-slate-200 dark:bg-slate-800 rounded-full text-xs truncate max-w-[200px] sm:max-w-xs">{chapterInfo?.name}</span>
        </div>

        <div className="flex bg-slate-200/50 dark:bg-slate-800 p-1 rounded-xl w-fit border border-slate-200 dark:border-slate-700">
          <button 
            onClick={() => setStudyMedium('english')} 
            className={`px-3 py-1.5 rounded-lg text-xs font-bold transition-all ${studyMedium === 'english' ? 'bg-white dark:bg-slate-700 text-indigo-600 dark:text-indigo-400 shadow-sm' : 'text-slate-600 dark:text-slate-400 hover:bg-white/50'}`}
          >
            English Medium
          </button>
          <button 
            onClick={() => setStudyMedium('kannada')} 
            className={`px-3 py-1.5 rounded-lg text-xs font-bold transition-all ${studyMedium === 'kannada' ? 'bg-white dark:bg-slate-700 text-indigo-600 dark:text-indigo-400 shadow-sm' : 'text-slate-600 dark:text-slate-400 hover:bg-white/50'}`}
          >
            ಕನ್ನಡ ಮಾಧ್ಯಮ
          </button>
        </div>
      </div>

      <header className={`relative overflow-hidden bg-gradient-to-br from-slate-900 to-slate-800 dark:from-[#0B1120] dark:to-slate-900 rounded-[2.5rem] p-8 md:p-12 text-white shadow-2xl shadow-slate-900/20 border border-slate-700`}>
        <div className={`absolute top-0 right-0 w-96 h-96 bg-gradient-to-bl ${theme.gradient} opacity-20 rounded-full blur-3xl -mr-20 -mt-20 pointer-events-none`}></div>
        <div className="relative z-10 max-w-3xl">
          <div className="flex flex-wrap gap-3 mb-6">
            <span className={`px-4 py-1.5 rounded-full text-sm font-bold backdrop-blur-md bg-white/10 border border-white/20`}>{subject?.name.split(' ')[0]}</span>
            <span className="px-4 py-1.5 rounded-full text-sm font-bold backdrop-blur-md bg-white/10 border border-white/20 text-amber-300">Board Weightage: {chapterInfo?.weightage}</span>
          </div>
          <h1 className="text-3xl md:text-5xl font-black mb-4 leading-tight">{chapterInfo?.name}</h1>
          <h2 className="text-xl md:text-2xl text-slate-400 font-medium">{chapterInfo?.kannadaName}</h2>
        </div>
      </header>

      <div className="flex flex-col lg:flex-row gap-8 items-start">
        <div className="flex-1 w-full">
          <div className="flex p-1.5 bg-slate-200/50 dark:bg-slate-800/50 rounded-2xl mb-8 overflow-x-auto hide-scrollbar border border-slate-200 dark:border-slate-800">
            {[
              { id: 'notes', icon: <BookOpen className="w-4 h-4 mr-2" />, label: 'Smart Notes' },
              { id: 'questions', icon: <FileText className="w-4 h-4 mr-2" />, label: 'Important Q&A' },
              { id: 'mcqs', icon: <Target className="w-4 h-4 mr-2" />, label: 'Practice Quiz' }
            ].map((tab) => (
              <button
                key={tab.id}
                onClick={() => setActiveTab(tab.id)}
                className={`flex-1 flex items-center justify-center whitespace-nowrap py-3 px-6 rounded-xl font-bold text-sm transition-all duration-300 ${
                  activeTab === tab.id 
                    ? 'bg-white dark:bg-slate-700 text-indigo-600 dark:text-indigo-400 shadow-sm' 
                    : 'text-slate-500 dark:text-slate-400 hover:text-slate-700 dark:hover:text-slate-200 hover:bg-slate-200 dark:hover:bg-slate-800'
                }`}
              >
                {tab.icon} {tab.label}
              </button>
            ))}
          </div>

          <div className="bg-white dark:bg-slate-800 rounded-[2.5rem] shadow-sm border border-slate-100 dark:border-slate-700 p-6 md:p-10 min-h-[500px]">
            {activeTab === 'notes' && <NotesTab content={chapterContentData.notes || []} theme={theme} />}
            {activeTab === 'questions' && <QuestionsTab questions={chapterContentData.questions || {}} />}
            {activeTab === 'mcqs' && <MCQsTab mcqs={chapterContentData.mcqs || []} />}
          </div>
        </div>

        <aside className="w-full lg:w-80 space-y-6 sticky top-24">
          <div className={`p-6 rounded-[2rem] border ${theme.bg} ${theme.border}`}>
            <h3 className={`font-black mb-3 flex items-center ${theme.text}`}>
              <Sparkles className="w-5 h-5 mr-2" /> Quick Summary
            </h3>
            <p className="text-sm text-slate-700 dark:text-slate-300 leading-relaxed font-medium">
              {chapterContentData.summary || 'No summary available.'}
            </p>
          </div>
        </aside>
      </div>
    </div>
  );
}

// --- SUBCOMPONENTS FOR CHAPTER TABS ---
function NotesTab({ content, theme }) {
  return (
    <div className="space-y-10 animate-fade-in">
      <div className="flex items-center justify-between pb-6 border-b border-slate-100 dark:border-slate-700">
        <h3 className="text-2xl font-black text-slate-900 dark:text-white">Chapter Notes</h3>
      </div>
      <div className="space-y-10">
        {content.map((note, index) => {
          // Fallback logic to support old data structure with singular 'imageUrl' or 'pdfLink'
          const imgs = note.imageUrls && note.imageUrls.length > 0 ? note.imageUrls : (note.imageUrl ? [note.imageUrl] : []);
          const pdfs = note.pdfLinks && note.pdfLinks.length > 0 ? note.pdfLinks : (note.pdfLink ? [note.pdfLink] : []);

          return (
            <div key={index} className="group">
              <h4 className="text-xl font-bold text-slate-900 dark:text-white mb-4 flex items-center">
                <span className={`w-8 h-8 rounded-full flex items-center justify-center text-sm mr-3 shrink-0 ${theme.bg} ${theme.text}`}>{index + 1}</span>
                {note.title}
              </h4>
              <div className="pl-11">
                <p className="text-slate-600 dark:text-slate-300 whitespace-pre-line leading-relaxed text-lg mb-4 font-medium">
                  {note.content}
                </p>
                
                {imgs.length > 0 && (
                  <div className="mb-4 space-y-4">
                    {imgs.map((imgUrl, idx) => (
                      imgUrl && (
                        <div key={idx} className="rounded-2xl overflow-hidden border border-slate-200 dark:border-slate-700 shadow-sm max-w-xl">
                          <img src={imgUrl} alt={`${note.title} - Image ${idx + 1}`} className="w-full h-auto object-cover" onError={(e) => { e.target.style.display = 'none'; }} />
                        </div>
                      )
                    ))}
                  </div>
                )}

                {note.example && (
                  <div className="bg-slate-50 dark:bg-slate-900/50 p-5 rounded-2xl border border-slate-200 dark:border-slate-700 text-slate-700 dark:text-slate-300 relative">
                    <div className="absolute top-0 left-0 w-1.5 h-full bg-slate-300 dark:bg-slate-600 rounded-l-2xl"></div>
                    <span className="font-bold text-slate-900 dark:text-white text-sm uppercase tracking-wider mb-2 block">Example</span>
                    <code className="font-mono text-[0.95rem]">{note.example}</code>
                  </div>
                )}

                {pdfs.length > 0 && (
                  <div className="mt-4 flex flex-wrap gap-3">
                    {pdfs.map((pdf, idx) => (
                      pdf && (
                        <a key={idx} href={pdf} target="_blank" rel="noreferrer" className="inline-flex items-center px-5 py-2.5 bg-indigo-50 dark:bg-indigo-900/30 text-indigo-600 dark:text-indigo-400 rounded-xl font-bold text-sm hover:bg-indigo-100 dark:hover:bg-indigo-900/50 transition-colors border border-indigo-100 dark:border-indigo-800/30 shadow-sm">
                          <FileText className="w-4 h-4 mr-2" /> View Attached PDF Note {pdfs.length > 1 ? idx + 1 : ''}
                        </a>
                      )
                    ))}
                  </div>
                )}
              </div>
            </div>
          );
        })}
        {content.length === 0 && <p className="text-slate-500">No notes available for this chapter.</p>}
      </div>
    </div>
  );
}

function QuestionsTab({ questions }) {
  const marksCategories = [
    { title: "1 Mark Questions", data: questions.marks1 || [], theme: "bg-emerald-50 text-emerald-700 border-emerald-200 dark:bg-emerald-900/20 dark:border-emerald-800/50 dark:text-emerald-400" },
    { title: "2 Marks Questions", data: questions.marks2 || [], theme: "bg-blue-50 text-blue-700 border-blue-200 dark:bg-blue-900/20 dark:border-blue-800/50 dark:text-blue-400" },
    { title: "3 Marks Questions", data: questions.marks3 || [], theme: "bg-purple-50 text-purple-700 border-purple-200 dark:bg-purple-900/20 dark:border-purple-800/50 dark:text-purple-400" },
    { title: "5 Marks (Long Answers)", data: questions.marks5 || [], theme: "bg-red-50 text-red-700 border-red-200 dark:bg-red-900/20 dark:border-red-800/50 dark:text-red-400" }
  ];

  return (
    <div className="space-y-12 animate-fade-in">
      <div className="pb-6 border-b border-slate-100 dark:border-slate-700">
        <h3 className="text-2xl font-black text-slate-900 dark:text-white">Exam Questions</h3>
      </div>
      {marksCategories.map((cat, idx) => (
        cat.data.length > 0 && (
          <div key={idx} className="mb-10">
            <div className={`inline-block px-5 py-2 rounded-full text-sm font-black border mb-6 ${cat.theme}`}>{cat.title}</div>
            <div className="space-y-6">
              {cat.data.map((item, qIdx) => (
                <div key={qIdx} className="bg-white dark:bg-slate-800 rounded-3xl p-6 border border-slate-200 dark:border-slate-700 shadow-sm">
                  <div className="flex gap-4 mb-4">
                    <div className="w-8 h-8 shrink-0 rounded-full bg-slate-100 dark:bg-slate-700 flex items-center justify-center font-bold text-slate-500">Q</div>
                    <p className="font-bold text-lg text-slate-900 dark:text-slate-100 mt-1">{item.q}</p>
                  </div>
                  <div className="flex gap-4">
                    <div className="w-8 h-8 shrink-0 rounded-full bg-indigo-50 dark:bg-indigo-900/30 flex items-center justify-center font-bold text-indigo-600 dark:text-indigo-400">A</div>
                    <div className="bg-slate-50 dark:bg-slate-900/50 p-5 rounded-2xl rounded-tl-none border border-slate-100 dark:border-slate-700 w-full">
                      <p className="text-slate-700 dark:text-slate-300 whitespace-pre-line leading-relaxed font-medium">{item.a}</p>
                    </div>
                  </div>
                </div>
              ))}
            </div>
          </div>
        )
      ))}
      {!marksCategories.some(c => c.data.length > 0) && <p className="text-slate-500">No questions available.</p>}
    </div>
  );
}

function MCQsTab({ mcqs }) {
  const [selectedAnswers, setSelectedAnswers] = useState({});
  const [showResults, setShowResults] = useState(false);
  const [errorMsg, setErrorMsg] = useState('');

  const handleSelect = (qIndex, optIndex) => { if (!showResults) setSelectedAnswers({ ...selectedAnswers, [qIndex]: optIndex }); };
  const calculateScore = () => {
    let score = 0;
    mcqs.forEach((q, i) => { if (selectedAnswers[i] === q.correct) score++; });
    return score;
  };

  const handleVerify = () => {
    if (Object.keys(selectedAnswers).length < mcqs.length) {
      setErrorMsg("Please answer all questions before checking answers!");
      return;
    }
    setErrorMsg("");
    setShowResults(true);
  };

  if (!mcqs || mcqs.length === 0) return <div className="text-center py-12 text-slate-500 font-medium">No MCQs added yet.</div>;

  return (
    <div className="animate-fade-in">
      <div className="flex flex-col sm:flex-row sm:items-center justify-between pb-6 border-b border-slate-100 dark:border-slate-700 mb-8 gap-4">
        <div><h3 className="text-2xl font-black text-slate-900 dark:text-white flex items-center">Interactive Quiz</h3></div>
        <div className="px-4 py-2 bg-slate-100 dark:bg-slate-800 rounded-xl text-sm font-bold text-slate-600 dark:text-slate-300">{mcqs.length} Questions</div>
      </div>

      <div className="space-y-12">
        {mcqs.map((q, qIndex) => (
          <div key={qIndex} className="bg-white dark:bg-slate-800">
            <p className="font-bold text-xl mb-6 text-slate-900 dark:text-slate-100 leading-snug"><span className="text-indigo-500 mr-2">{qIndex + 1}.</span> {q.question}</p>
            <div className="grid grid-cols-1 sm:grid-cols-2 gap-4">
              {q.options.map((opt, optIndex) => {
                const isSelected = selectedAnswers[qIndex] === optIndex;
                const isCorrect = q.correct === optIndex;
                let btnClass = "relative w-full text-left px-6 py-4 rounded-2xl font-bold transition-all duration-200 border-2 outline-none group ";
                if (!showResults) {
                  btnClass += isSelected ? "border-indigo-500 bg-indigo-50 dark:bg-indigo-900/20 text-indigo-700 shadow-[0_4px_0_rgb(99,102,241)] translate-y-1" : "border-slate-200 dark:border-slate-700 bg-white dark:bg-slate-800 text-slate-700 dark:text-slate-300 hover:border-indigo-300 shadow-[0_6px_0_rgb(226,232,240)] dark:shadow-[0_6px_0_rgb(51,65,85)]";
                } else {
                  if (isCorrect) btnClass += "border-emerald-500 bg-emerald-50 dark:bg-emerald-900/20 text-emerald-700 shadow-[0_4px_0_rgb(16,185,129)]";
                  else if (isSelected) btnClass += "border-red-500 bg-red-50 dark:bg-red-900/20 text-red-700 shadow-[0_4px_0_rgb(239,68,68)]";
                  else btnClass += "border-slate-200 dark:border-slate-700 text-slate-400 opacity-50 bg-slate-50 dark:bg-slate-900 shadow-none translate-y-1";
                }
                return (
                  <button key={optIndex} onClick={() => handleSelect(qIndex, optIndex)} className={btnClass} disabled={showResults}>
                    <div className="flex items-center">
                      <span className={`w-8 h-8 rounded-full flex items-center justify-center text-sm mr-4 shrink-0 transition-colors ${!showResults && isSelected ? 'bg-indigo-500 text-white' : showResults && isCorrect ? 'bg-emerald-500 text-white' : showResults && isSelected && !isCorrect ? 'bg-red-500 text-white' : 'bg-slate-100 dark:bg-slate-700 text-slate-500'}`}>{String.fromCharCode(65 + optIndex)}</span>
                      <span className="leading-tight">{opt}</span>
                    </div>
                  </button>
                );
              })}
            </div>
            {showResults && (
              <div className={`mt-6 p-5 rounded-2xl font-bold flex items-center border ${selectedAnswers[qIndex] === q.correct ? 'bg-emerald-50 text-emerald-800 border-emerald-200' : 'bg-red-50 text-red-800 border-red-200'}`}>
                {selectedAnswers[qIndex] === q.correct ? "✅ Correct!" : `❌ Incorrect. Right answer is Option ${String.fromCharCode(65 + q.correct)}.`}
              </div>
            )}
          </div>
        ))}
      </div>

      <div className="mt-12 pt-8 border-t border-slate-100 dark:border-slate-800">
        {!showResults ? (
          <>
            {errorMsg && <p className="text-red-500 font-bold text-center mb-4">{errorMsg}</p>}
            <button onClick={handleVerify} className="w-full sm:w-auto bg-slate-900 dark:bg-white text-white dark:text-slate-900 font-black py-4 px-10 rounded-full transition-all shadow-xl hover:-translate-y-1 text-lg mx-auto block">Check Answers</button>
          </>
        ) : (
          <div className="bg-slate-50 dark:bg-slate-900/50 p-8 rounded-[2.5rem] text-center border border-slate-200 dark:border-slate-700">
            <h4 className="text-slate-500 font-bold uppercase tracking-widest mb-2">Quiz Completed</h4>
            <div className="text-5xl font-black mb-8 text-slate-900 dark:text-white">Score: <span className="text-indigo-600">{calculateScore()}</span>/{mcqs.length}</div>
            <button onClick={() => { setSelectedAnswers({}); setShowResults(false); }} className="bg-white dark:bg-slate-800 text-slate-900 dark:text-white border border-slate-200 font-bold py-3 px-8 rounded-full shadow-sm">Try Again</button>
          </div>
        )}
      </div>
    </div>
  );
}

// --- ADMIN COMPONENTS ---
function AdminLogin({ navigateTo, setIsAdmin, showToast }) {
  const [password, setPassword] = useState('');

  const handleLogin = (e) => {
    e.preventDefault();
    if (password === '@Suraj9066') { setIsAdmin(true); navigateTo('admin_dashboard'); showToast('Welcome to Admin Portal'); } 
    else { showToast('Invalid Admin Password'); }
  };

  return (
    <div className="max-w-md mx-auto mt-20 p-10 bg-white dark:bg-slate-800 rounded-[2.5rem] shadow-2xl border border-slate-100 dark:border-slate-700 animate-fade-in relative overflow-hidden">
      <div className="absolute top-0 left-0 w-full h-2 bg-gradient-to-r from-indigo-500 to-purple-500"></div>
      <div className="text-center mb-10">
        <div className="w-16 h-16 bg-indigo-50 dark:bg-indigo-900/30 rounded-2xl flex items-center justify-center mx-auto mb-6 rotate-3"><Lock className="w-8 h-8 text-indigo-600 dark:text-indigo-400" /></div>
        <h2 className="text-3xl font-black text-slate-900 dark:text-white">Admin Portal</h2>
      </div>
      <form onSubmit={handleLogin} className="space-y-6">
        <input type="password" value={password} onChange={(e) => setPassword(e.target.value)} className="w-full bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 rounded-2xl px-5 py-4 focus:ring-2 focus:ring-indigo-500 font-medium" placeholder="Enter password..."/>
        <button type="submit" className="w-full bg-indigo-600 hover:bg-indigo-700 text-white font-black py-4 rounded-2xl transition-all shadow-lg hover:-translate-y-1">Unlock Dashboard</button>
        <button type="button" onClick={() => navigateTo('home')} className="w-full text-slate-500 hover:text-slate-700 font-bold text-sm py-2">Return Home</button>
      </form>
    </div>
  );
}

function AdminDashboard({ navigateTo, appData, setAppData, isAdmin, showToast, setConfirmDialog }) {
  const [adminTab, setAdminTab] = useState('homepage');
  
  // Home Page Settings State
  const [hpForm, setHpForm] = useState(appData.homePage);
  const handleHpSave = () => { setAppData({...appData, homePage: hpForm}); showToast('Homepage settings saved successfully!'); };

  // Chapter Settings State
  const [selectedSubject, setSelectedSubject] = useState('science');
  const [newChapterName, setNewChapterName] = useState('');
  
  // Visual Editor State
  const [editingContentId, setEditingContentId] = useState(null);
  const [chapterForm, setChapterForm] = useState(null);
  const [editMedium, setEditMedium] = useState('english'); // Internal admin medium toggle

  // PYQ Settings State
  const [newPyq, setNewPyq] = useState({ year: '', title: '', link: '' });

  if (!isAdmin) return <div className="text-center py-20 text-red-500 font-black text-2xl">Access Denied.</div>;

  const handleAddChapter = () => {
    if (!newChapterName) return showToast("Chapter name is required.");
    const newId = `${selectedSubject}_ch${Date.now()}`;
    const newChapter = { id: newId, name: newChapterName, kannadaName: 'ಹೊಸ ಅಧ್ಯಾಯ', weightage: '0 Marks' };
    const updatedChapters = { ...appData.chapters, [selectedSubject]: [...(appData.chapters[selectedSubject] || []), newChapter] };
    
    // Create new dual-medium structure for blank chapter with arrays for links
    const updatedContent = { 
      ...appData.chapterContent, 
      [newId]: { 
        english: { notes: [], summary: "New summary...", questions: { marks1: [], marks2: [], marks3: [], marks5: [] }, mcqs: [] },
        kannada: { notes: [], summary: "ಹೊಸ ಸಾರಾಂಶ...", questions: { marks1: [], marks2: [], marks3: [], marks5: [] }, mcqs: [] }
      } 
    };
    setAppData({ ...appData, chapters: updatedChapters, chapterContent: updatedContent });
    setNewChapterName('');
    showToast('Chapter created successfully!');
  };

  const startEditing = (chapterId) => {
    setEditingContentId(chapterId);
    let existingData = appData.chapterContent[chapterId];
    
    // Migrate old format to dual-medium format if needed
    if (existingData && !existingData.english) {
       existingData = {
         english: { ...JSON.parse(JSON.stringify(existingData)) },
         kannada: { notes: [], summary: "", questions: {marks1:[], marks2:[], marks3:[], marks5:[]}, mcqs: [] }
       };
    } else if (!existingData) {
       existingData = {
         english: { notes: [], summary: "", questions: {marks1:[], marks2:[], marks3:[], marks5:[]}, mcqs: [] },
         kannada: { notes: [], summary: "", questions: {marks1:[], marks2:[], marks3:[], marks5:[]}, mcqs: [] }
       };
    }

    // Auto-migrate old singular properties (imageUrl / pdfLink) to multiple arrays
    ['english', 'kannada'].forEach(lang => {
      if (existingData[lang] && existingData[lang].notes) {
        existingData[lang].notes = existingData[lang].notes.map(n => ({
          ...n,
          imageUrls: n.imageUrls || (n.imageUrl ? [n.imageUrl] : []),
          pdfLinks: n.pdfLinks || (n.pdfLink ? [n.pdfLink] : [])
        }));
      }
    });
    
    setChapterForm(JSON.parse(JSON.stringify(existingData)));
    setEditMedium('english');
  };

  const saveChapterContent = () => {
    setAppData({ ...appData, chapterContent: { ...appData.chapterContent, [editingContentId]: chapterForm } });
    setEditingContentId(null);
    showToast('Chapter content saved successfully!');
  };

  const updateMediumContent = (key, value) => {
    setChapterForm({
      ...chapterForm,
      [editMedium]: {
        ...chapterForm[editMedium],
        [key]: value
      }
    });
  };

  const deleteChapter = (chapterId) => {
     setConfirmDialog({
       message: "Are you sure you want to permanently delete this chapter?",
       onConfirm: () => {
         setAppData({...appData, chapters: { ...appData.chapters, [selectedSubject]: appData.chapters[selectedSubject].filter(c => c.id !== chapterId) }});
         showToast('Chapter deleted.');
       }
     });
  };

  const handleAddPyq = () => {
    if (!newPyq.title || !newPyq.link) return showToast("Title and link are required!");
    const addedPyq = { ...newPyq, id: `pyq_${Date.now()}` };
    setAppData({ ...appData, pyqs: [...(appData.pyqs || []), addedPyq] });
    setNewPyq({ year: '', title: '', link: '' });
    showToast('Question paper added!');
  };

  const deletePyq = (id) => {
    setConfirmDialog({
      message: "Are you sure you want to remove this question paper?",
      onConfirm: () => {
        setAppData({...appData, pyqs: (appData.pyqs || []).filter(p => p.id !== id)});
        showToast('Paper removed.');
      }
    });
  };

  return (
    <div className="animate-fade-in max-w-6xl mx-auto space-y-8">
      <div className="flex flex-col sm:flex-row justify-between items-center bg-slate-900 rounded-[2rem] p-8 text-white shadow-xl">
        <h1 className="text-3xl font-black flex items-center mb-4 sm:mb-0"><Edit className="w-8 h-8 mr-4 text-indigo-400" /> Control Panel</h1>
        <button onClick={() => navigateTo('home')} className="bg-white/10 hover:bg-white/20 px-6 py-3 rounded-full font-bold transition backdrop-blur-md text-sm">Exit Admin</button>
      </div>

      <div className="flex p-1.5 bg-white dark:bg-slate-800 rounded-2xl shadow-sm border border-slate-200 dark:border-slate-700 overflow-x-auto hide-scrollbar">
        <button onClick={() => setAdminTab('homepage')} className={`flex-1 px-8 py-3 rounded-xl font-bold transition-all flex justify-center items-center ${adminTab === 'homepage' ? 'bg-indigo-600 text-white shadow-md' : 'text-slate-600 dark:text-slate-400 hover:bg-slate-100 dark:hover:bg-slate-700'}`}><Home className="w-4 h-4 mr-2"/> Home Page</button>
        <button onClick={() => setAdminTab('chapters')} className={`flex-1 px-8 py-3 rounded-xl font-bold transition-all flex justify-center items-center ${adminTab === 'chapters' ? 'bg-indigo-600 text-white shadow-md' : 'text-slate-600 dark:text-slate-400 hover:bg-slate-100 dark:hover:bg-slate-700'}`}><LayoutDashboard className="w-4 h-4 mr-2"/> Chapters</button>
        <button onClick={() => setAdminTab('pyqs')} className={`flex-1 px-8 py-3 rounded-xl font-bold transition-all flex justify-center items-center ${adminTab === 'pyqs' ? 'bg-indigo-600 text-white shadow-md' : 'text-slate-600 dark:text-slate-400 hover:bg-slate-100 dark:hover:bg-slate-700'}`}><FileText className="w-4 h-4 mr-2"/> Papers</button>
      </div>

      {/* --- HOMEPAGE EDITOR TAB --- */}
      {adminTab === 'homepage' && (
        <div className="bg-white dark:bg-slate-800 p-8 rounded-[2rem] shadow-sm border border-slate-200 dark:border-slate-700 animate-fade-in">
          <h3 className="text-2xl font-black mb-6 border-b pb-4 dark:border-slate-700">Hero Section Text</h3>
          <div className="grid md:grid-cols-2 gap-6 mb-8">
            <div><label className="block text-sm font-bold mb-2">Badge Text (Top)</label><input value={hpForm.heroBadge} onChange={e=>setHpForm({...hpForm, heroBadge: e.target.value})} className="w-full bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 p-3 rounded-xl outline-none focus:ring-2 focus:ring-indigo-500" /></div>
            <div><label className="block text-sm font-bold mb-2">Main Title (Line 1)</label><input value={hpForm.heroTitleLine1} onChange={e=>setHpForm({...hpForm, heroTitleLine1: e.target.value})} className="w-full bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 p-3 rounded-xl outline-none focus:ring-2 focus:ring-indigo-500" /></div>
            <div><label className="block text-sm font-bold mb-2">Main Title (Gradient Line 2)</label><input value={hpForm.heroTitleLine2} onChange={e=>setHpForm({...hpForm, heroTitleLine2: e.target.value})} className="w-full bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 p-3 rounded-xl outline-none focus:ring-2 focus:ring-indigo-500" /></div>
            <div className="md:col-span-2"><label className="block text-sm font-bold mb-2">Subtitle / Description</label><textarea value={hpForm.heroSubtitle} onChange={e=>setHpForm({...hpForm, heroSubtitle: e.target.value})} className="w-full bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 p-3 rounded-xl outline-none focus:ring-2 focus:ring-indigo-500" rows="2" /></div>
          </div>

          <h3 className="text-2xl font-black mb-6 border-b pb-4 dark:border-slate-700">Latest Updates Section</h3>
          <div className="space-y-3 mb-8">
            {hpForm.updates.map((upd, i) => (
               <div key={i} className="flex gap-2">
                 <input value={upd} onChange={(e) => { const n = [...hpForm.updates]; n[i] = e.target.value; setHpForm({...hpForm, updates: n}) }} className="flex-1 bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 p-3 rounded-xl outline-none" />
                 <button onClick={() => { const n = hpForm.updates.filter((_, idx)=>idx!==i); setHpForm({...hpForm, updates: n}) }} className="p-3 bg-red-100 text-red-600 rounded-xl hover:bg-red-200"><Trash2 className="w-5 h-5"/></button>
               </div>
            ))}
            <button onClick={() => setHpForm({...hpForm, updates: [...hpForm.updates, "New Update Item"]})} className="text-sm font-bold text-indigo-600 flex items-center mt-2"><Plus className="w-4 h-4 mr-1"/> Add Update Line</button>
          </div>
          
          <button onClick={handleHpSave} className="bg-indigo-600 text-white font-bold py-4 px-8 rounded-xl shadow-lg hover:bg-indigo-700 flex items-center"><Save className="w-5 h-5 mr-2" /> Save Home Page Changes</button>
        </div>
      )}

      {/* --- CHAPTER MANAGER TAB --- */}
      {adminTab === 'chapters' && (
        <div className="grid lg:grid-cols-3 gap-8">
          <div className="lg:col-span-1 space-y-6">
            <div className="bg-white dark:bg-slate-800 p-6 rounded-[2rem] shadow-sm border border-slate-200 dark:border-slate-700">
              <h3 className="font-bold mb-4 text-slate-900 dark:text-white uppercase tracking-wider text-xs">1. Select Subject</h3>
              <select value={selectedSubject} onChange={(e) => setSelectedSubject(e.target.value)} className="w-full bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 rounded-xl p-3 font-medium focus:ring-2 focus:ring-indigo-500 outline-none">
                {appData.subjects.map(sub => <option key={sub.id} value={sub.id}>{sub.name}</option>)}
              </select>
            </div>
            <div className="bg-white dark:bg-slate-800 p-6 rounded-[2rem] shadow-sm border border-slate-200 dark:border-slate-700">
              <h3 className="font-bold mb-4 text-slate-900 dark:text-white uppercase tracking-wider text-xs">2. Add New Chapter</h3>
              <input type="text" value={newChapterName} onChange={(e) => setNewChapterName(e.target.value)} placeholder="e.g., 2. Human Eye" className="w-full bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 rounded-xl p-3 mb-4 outline-none focus:ring-2 focus:ring-indigo-500 font-medium"/>
              <button onClick={handleAddChapter} className="w-full bg-slate-900 dark:bg-white text-white dark:text-slate-900 font-bold py-3 rounded-xl flex items-center justify-center transition-transform hover:-translate-y-0.5"><Plus className="w-5 h-5 mr-1" /> Add Chapter</button>
            </div>
          </div>

          <div className="lg:col-span-2 bg-white dark:bg-slate-800 p-8 rounded-[2rem] shadow-sm border border-slate-200 dark:border-slate-700">
            {editingContentId && chapterForm ? (
              <div className="animate-fade-in">
                <div className="flex flex-col sm:flex-row justify-between items-start sm:items-center mb-6 pb-4 border-b dark:border-slate-700 gap-4">
                  <h3 className="text-xl font-black text-indigo-600 dark:text-indigo-400 flex items-center"><Edit className="w-5 h-5 mr-2"/> Visual Editor</h3>
                  
                  <div className="flex items-center gap-4">
                    {/* Admin Medium Toggle */}
                    <div className="flex bg-slate-200 dark:bg-slate-700 p-1 rounded-xl">
                      <button onClick={() => setEditMedium('english')} className={`px-4 py-1.5 rounded-lg text-sm font-bold transition-all ${editMedium === 'english' ? 'bg-white text-indigo-600 shadow' : 'text-slate-600 dark:text-slate-300 hover:bg-slate-300 dark:hover:bg-slate-600'}`}>English</button>
                      <button onClick={() => setEditMedium('kannada')} className={`px-4 py-1.5 rounded-lg text-sm font-bold transition-all ${editMedium === 'kannada' ? 'bg-white text-indigo-600 shadow' : 'text-slate-600 dark:text-slate-300 hover:bg-slate-300 dark:hover:bg-slate-600'}`}>Kannada</button>
                    </div>
                    <button onClick={() => setEditingContentId(null)} className="text-red-500 text-sm font-bold bg-red-50 dark:bg-red-900/20 px-4 py-2 rounded-xl hover:bg-red-100">Cancel</button>
                  </div>
                </div>

                <div className="space-y-8 max-h-[60vh] overflow-y-auto pr-4 custom-scrollbar">
                  <div>
                    <label className="block font-bold mb-2 text-slate-700 dark:text-slate-300">Chapter Summary ({editMedium === 'english' ? 'English' : 'Kannada'})</label>
                    <textarea value={chapterForm[editMedium].summary} onChange={e=>updateMediumContent('summary', e.target.value)} className="w-full bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 p-3 rounded-xl" rows="3" />
                  </div>

                  <div className="bg-slate-50 dark:bg-slate-900/50 p-6 rounded-2xl border border-slate-200 dark:border-slate-700">
                    <h4 className="font-bold mb-4 flex items-center"><BookOpen className="w-5 h-5 mr-2"/> Notes & Resources</h4>
                    {chapterForm[editMedium].notes.map((note, i) => (
                      <div key={i} className="mb-6 p-4 bg-white dark:bg-slate-800 rounded-xl shadow-sm border border-slate-200 dark:border-slate-700 space-y-3">
                        <div className="flex justify-between">
                           <span className="font-bold text-xs bg-slate-200 dark:bg-slate-700 px-2 py-1 rounded">Note block {i+1}</span>
                           <button onClick={()=>{ const n = [...chapterForm[editMedium].notes]; n.splice(i,1); updateMediumContent('notes', n); }} className="text-red-500 text-xs font-bold hover:underline">Remove Block</button>
                        </div>
                        <input value={note.title} onChange={e=>{ const n = [...chapterForm[editMedium].notes]; n[i] = {...n[i], title: e.target.value}; updateMediumContent('notes', n); }} placeholder="Title / Heading" className="w-full bg-slate-50 dark:bg-slate-900 border p-2 rounded-lg font-bold" />
                        <textarea value={note.content} onChange={e=>{ const n = [...chapterForm[editMedium].notes]; n[i] = {...n[i], content: e.target.value}; updateMediumContent('notes', n); }} placeholder="Main Content Text" className="w-full bg-slate-50 dark:bg-slate-900 border p-2 rounded-lg" rows="3" />
                        
                        {/* Multiple Images Editor */}
                        <div className="space-y-2 mt-4 bg-slate-100 dark:bg-slate-900 p-3 rounded-xl border border-slate-200 dark:border-slate-700">
                          <div className="flex justify-between items-center">
                            <label className="text-sm font-bold text-slate-600 dark:text-slate-400 flex items-center"><ImageIcon className="w-4 h-4 mr-2"/> Images</label>
                            <button onClick={()=>{
                               const n = [...chapterForm[editMedium].notes];
                               n[i] = {...n[i], imageUrls: [...(n[i].imageUrls || []), ""]};
                               updateMediumContent('notes', n);
                            }} className="text-xs font-bold text-indigo-600 bg-indigo-50 dark:bg-indigo-900/30 px-3 py-1.5 rounded-lg hover:bg-indigo-100 dark:hover:bg-indigo-900/50 transition-colors">+ Add Image</button>
                          </div>
                          {(note.imageUrls || []).map((url, imgIdx) => (
                            <div key={imgIdx} className="flex gap-2 items-center">
                               <input value={url} onChange={e => {
                                 const n = [...chapterForm[editMedium].notes];
                                 const urls = [...(n[i].imageUrls || [])];
                                 urls[imgIdx] = e.target.value;
                                 n[i] = {...n[i], imageUrls: urls};
                                 updateMediumContent('notes', n);
                               }} className="flex-1 bg-white dark:bg-slate-800 border border-slate-200 dark:border-slate-700 p-2 rounded-lg text-sm text-indigo-500 focus:ring-2 focus:ring-indigo-500 outline-none" placeholder="Paste Image URL here..." />
                               <button onClick={()=>{
                                 const n = [...chapterForm[editMedium].notes];
                                 const urls = [...(n[i].imageUrls || [])];
                                 urls.splice(imgIdx, 1);
                                 n[i] = {...n[i], imageUrls: urls};
                                 updateMediumContent('notes', n);
                               }} className="text-red-500 p-2 hover:bg-red-50 dark:hover:bg-red-900/20 rounded-lg transition-colors"><Trash2 className="w-4 h-4"/></button>
                            </div>
                          ))}
                          {(!note.imageUrls || note.imageUrls.length === 0) && <p className="text-xs text-slate-400 font-medium pb-1">No images attached.</p>}
                        </div>

                        {/* Multiple PDFs Editor */}
                        <div className="space-y-2 mt-4 bg-slate-100 dark:bg-slate-900 p-3 rounded-xl border border-slate-200 dark:border-slate-700">
                          <div className="flex justify-between items-center">
                            <label className="text-sm font-bold text-slate-600 dark:text-slate-400 flex items-center"><FileText className="w-4 h-4 mr-2"/> PDFs / Documents</label>
                            <button onClick={()=>{
                               const n = [...chapterForm[editMedium].notes];
                               n[i] = {...n[i], pdfLinks: [...(n[i].pdfLinks || []), ""]};
                               updateMediumContent('notes', n);
                            }} className="text-xs font-bold text-indigo-600 bg-indigo-50 dark:bg-indigo-900/30 px-3 py-1.5 rounded-lg hover:bg-indigo-100 dark:hover:bg-indigo-900/50 transition-colors">+ Add PDF</button>
                          </div>
                          {(note.pdfLinks || []).map((pdf, pdfIdx) => (
                            <div key={pdfIdx} className="flex gap-2 items-center">
                               <input value={pdf} onChange={e => {
                                 const n = [...chapterForm[editMedium].notes];
                                 const pdfs = [...(n[i].pdfLinks || [])];
                                 pdfs[pdfIdx] = e.target.value;
                                 n[i] = {...n[i], pdfLinks: pdfs};
                                 updateMediumContent('notes', n);
                               }} className="flex-1 bg-white dark:bg-slate-800 border border-slate-200 dark:border-slate-700 p-2 rounded-lg text-sm text-indigo-500 focus:ring-2 focus:ring-indigo-500 outline-none" placeholder="Paste PDF/Drive Link here..." />
                               <button onClick={()=>{
                                 const n = [...chapterForm[editMedium].notes];
                                 const pdfs = [...(n[i].pdfLinks || [])];
                                 pdfs.splice(pdfIdx, 1);
                                 n[i] = {...n[i], pdfLinks: pdfs};
                                 updateMediumContent('notes', n);
                               }} className="text-red-500 p-2 hover:bg-red-50 dark:hover:bg-red-900/20 rounded-lg transition-colors"><Trash2 className="w-4 h-4"/></button>
                            </div>
                          ))}
                          {(!note.pdfLinks || note.pdfLinks.length === 0) && <p className="text-xs text-slate-400 font-medium pb-1">No PDFs attached.</p>}
                        </div>

                      </div>
                    ))}
                    <button onClick={() => updateMediumContent('notes', [...chapterForm[editMedium].notes, {title:"", content:"", example:"", imageUrls:[], pdfLinks:[]}])} className="text-sm font-bold text-indigo-600 flex items-center bg-indigo-50 px-4 py-3 rounded-xl hover:bg-indigo-100 transition-colors"><Plus className="w-5 h-5 mr-1"/> Add Note Block</button>
                  </div>

                  <div className="bg-slate-50 dark:bg-slate-900/50 p-6 rounded-2xl border border-slate-200 dark:border-slate-700">
                    <h4 className="font-bold mb-4 flex items-center"><BookOpen className="w-5 h-5 mr-2"/> Notes & Images</h4>
                    {chapterForm[editMedium].notes.map((note, i) => (
                      <div key={i} className="mb-6 p-4 bg-white dark:bg-slate-800 rounded-xl shadow-sm border border-slate-200 dark:border-slate-700 space-y-3">
                        <div className="flex justify-between">
                           <span className="font-bold text-xs bg-slate-200 dark:bg-slate-700 px-2 py-1 rounded">Note block {i+1}</span>
                           <button onClick={()=>{ const n = [...chapterForm[editMedium].notes]; n.splice(i,1); updateMediumContent('notes', n); }} className="text-red-500 text-xs font-bold hover:underline">Remove</button>
                        </div>
                        <input value={note.title} onChange={e=>{ const n = [...chapterForm[editMedium].notes]; n[i] = {...n[i], title: e.target.value}; updateMediumContent('notes', n); }} placeholder="Title / Heading" className="w-full bg-slate-50 dark:bg-slate-900 border p-2 rounded-lg" />
                        <textarea value={note.content} onChange={e=>{ const n = [...chapterForm[editMedium].notes]; n[i] = {...n[i], content: e.target.value}; updateMediumContent('notes', n); }} placeholder="Main Content Text" className="w-full bg-slate-50 dark:bg-slate-900 border p-2 rounded-lg" rows="3" />
                        <div className="flex gap-2 items-center">
                           <ImageIcon className="w-5 h-5 text-slate-400 shrink-0" />
                           <input value={note.imageUrl || ""} onChange={e=>{ const n = [...chapterForm[editMedium].notes]; n[i] = {...n[i], imageUrl: e.target.value}; updateMediumContent('notes', n); }} placeholder="Paste Image URL here (Optional)" className="w-full bg-slate-50 dark:bg-slate-900 border p-2 rounded-lg text-sm text-indigo-500" />
                        </div>
                      </div>
                    ))}
                    <button onClick={() => updateMediumContent('notes', [...chapterForm[editMedium].notes, {title:"", content:"", example:"", imageUrl:""}])} className="text-sm font-bold text-indigo-600 flex items-center bg-indigo-50 px-4 py-2 rounded-lg"><Plus className="w-4 h-4 mr-1"/> Add Note Block</button>
                  </div>

                  <div className="bg-slate-50 dark:bg-slate-900/50 p-6 rounded-2xl border border-slate-200 dark:border-slate-700">
                    <h4 className="font-bold mb-4 flex items-center"><Target className="w-5 h-5 mr-2"/> MCQ Quiz Editor</h4>
                    {chapterForm[editMedium].mcqs.map((mcq, i) => (
                      <div key={i} className="mb-6 p-4 bg-white dark:bg-slate-800 rounded-xl shadow-sm border border-slate-200 dark:border-slate-700 space-y-3">
                         <div className="flex justify-between">
                           <span className="font-bold text-xs bg-slate-200 dark:bg-slate-700 px-2 py-1 rounded">Question {i+1}</span>
                           <button onClick={()=>{ const m = [...chapterForm[editMedium].mcqs]; m.splice(i,1); updateMediumContent('mcqs', m); }} className="text-red-500 text-xs font-bold hover:underline">Remove</button>
                        </div>
                        <input value={mcq.question} onChange={e=>{ const m = [...chapterForm[editMedium].mcqs]; m[i] = {...m[i], question: e.target.value}; updateMediumContent('mcqs', m); }} placeholder="Question?" className="w-full bg-slate-50 dark:bg-slate-900 border p-2 rounded-lg font-bold" />
                        <div className="grid grid-cols-2 gap-2">
                           {[0,1,2,3].map(optIdx => (
                             <input key={optIdx} value={mcq.options[optIdx] || ""} onChange={e=>{ 
                               const m = [...chapterForm[editMedium].mcqs]; 
                               const newOpts = [...m[i].options];
                               newOpts[optIdx] = e.target.value;
                               m[i] = {...m[i], options: newOpts}; 
                               updateMediumContent('mcqs', m); 
                             }} placeholder={`Option ${String.fromCharCode(65+optIdx)}`} className={`bg-slate-50 dark:bg-slate-900 border p-2 rounded-lg text-sm ${mcq.correct === optIdx ? 'border-emerald-500 ring-1 ring-emerald-500' : ''}`} />
                           ))}
                        </div>
                        <div className="flex items-center gap-2 mt-2">
                          <label className="text-sm font-bold">Correct Answer Index (0=A, 1=B, 2=C, 3=D):</label>
                          <input type="number" min="0" max="3" value={mcq.correct} onChange={e=>{ const m = [...chapterForm[editMedium].mcqs]; m[i] = {...m[i], correct: parseInt(e.target.value) || 0}; updateMediumContent('mcqs', m); }} className="w-16 bg-slate-50 dark:bg-slate-900 border p-1 rounded-lg text-center font-bold text-emerald-600" />
                        </div>
                      </div>
                    ))}
                    <button onClick={() => updateMediumContent('mcqs', [...chapterForm[editMedium].mcqs, {question:"", options:["","","",""], correct:0}])} className="text-sm font-bold text-indigo-600 flex items-center bg-indigo-50 px-4 py-2 rounded-lg"><Plus className="w-4 h-4 mr-1"/> Add MCQ Question</button>
                  </div>

                </div>
                <div className="mt-8 pt-6 border-t dark:border-slate-700">
                  <button onClick={saveChapterContent} className="bg-indigo-600 hover:bg-indigo-700 text-white font-black py-4 px-8 rounded-xl flex items-center justify-center transition shadow-lg w-full"><Save className="w-5 h-5 mr-2" /> Save Content</button>
                </div>
              </div>
            ) : (
              <div>
                <h3 className="text-2xl font-black mb-6 text-slate-900 dark:text-white">{appData.subjects.find(s => s.id === selectedSubject)?.name} Content</h3>
                <div className="space-y-4">
                  {(appData.chapters[selectedSubject] || []).map((ch, i) => (
                    <div key={ch.id} className="flex flex-col sm:flex-row sm:items-center justify-between p-5 bg-slate-50 dark:bg-slate-900 rounded-2xl border border-slate-200 dark:border-slate-700">
                      <div className="mb-4 sm:mb-0">
                        <p className="font-bold text-slate-900 dark:text-white text-lg"><span className="text-slate-400 mr-2">{i+1}.</span>{ch.name}</p>
                      </div>
                      <div className="flex space-x-2">
                        <button onClick={() => startEditing(ch.id)} className="px-5 py-2.5 bg-indigo-100 text-indigo-700 dark:bg-indigo-900/40 dark:text-indigo-300 rounded-xl hover:bg-indigo-200 font-bold transition text-sm">Visual Editor</button>
                        <button onClick={() => deleteChapter(ch.id)} className="p-2.5 bg-red-100 text-red-700 dark:bg-red-900/40 dark:text-red-300 rounded-xl hover:bg-red-200 transition"><Trash2 className="w-5 h-5" /></button>
                      </div>
                    </div>
                  ))}
                  {(!appData.chapters[selectedSubject] || appData.chapters[selectedSubject].length === 0) && (
                    <div className="text-center py-16 border-2 border-dashed border-slate-200 dark:border-slate-700 rounded-2xl bg-slate-50 dark:bg-slate-900/50">
                      <p className="text-slate-500 font-medium">Empty subject. Add a chapter first.</p>
                    </div>
                  )}
                </div>
              </div>
            )}
          </div>
        </div>
      )}

      {/* --- PYQ MANAGER TAB --- */}
      {adminTab === 'pyqs' && (
        <div className="grid lg:grid-cols-3 gap-8 animate-fade-in">
          <div className="lg:col-span-1">
            <div className="bg-white dark:bg-slate-800 p-6 rounded-[2rem] shadow-sm border border-slate-200 dark:border-slate-700">
              <h3 className="font-bold mb-6 text-slate-900 dark:text-white uppercase tracking-wider text-xs">Add New Question Paper</h3>
              <div className="space-y-4">
                <div>
                  <label className="block text-sm font-bold mb-1 text-slate-600 dark:text-slate-400">Year (e.g., 2024)</label>
                  <input type="text" value={newPyq.year} onChange={(e) => setNewPyq({...newPyq, year: e.target.value})} className="w-full bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 p-3 rounded-xl outline-none focus:ring-2 focus:ring-indigo-500 font-medium" />
                </div>
                <div>
                  <label className="block text-sm font-bold mb-1 text-slate-600 dark:text-slate-400">Paper Title</label>
                  <input type="text" value={newPyq.title} onChange={(e) => setNewPyq({...newPyq, title: e.target.value})} placeholder="e.g., Science Main Exam" className="w-full bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 p-3 rounded-xl outline-none focus:ring-2 focus:ring-indigo-500 font-medium" />
                </div>
                <div>
                  <label className="block text-sm font-bold mb-1 text-slate-600 dark:text-slate-400">PDF / Drive Link</label>
                  <input type="url" value={newPyq.link} onChange={(e) => setNewPyq({...newPyq, link: e.target.value})} placeholder="https://..." className="w-full bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 p-3 rounded-xl outline-none focus:ring-2 focus:ring-indigo-500 font-medium text-indigo-500" />
                </div>
                <button onClick={handleAddPyq} className="w-full bg-indigo-600 hover:bg-indigo-700 text-white font-bold py-3 rounded-xl flex items-center justify-center transition-transform hover:-translate-y-0.5 mt-2 shadow-lg"><Plus className="w-5 h-5 mr-1" /> Add Paper</button>
              </div>
            </div>
          </div>

          <div className="lg:col-span-2 bg-white dark:bg-slate-800 p-8 rounded-[2rem] shadow-sm border border-slate-200 dark:border-slate-700">
             <h3 className="text-2xl font-black mb-6 text-slate-900 dark:text-white">Uploaded Papers</h3>
             <div className="space-y-4">
                {(appData.pyqs || []).map((pyq) => (
                  <div key={pyq.id} className="flex flex-col sm:flex-row sm:items-center justify-between p-5 bg-slate-50 dark:bg-slate-900 rounded-2xl border border-slate-200 dark:border-slate-700">
                    <div className="mb-4 sm:mb-0">
                      <p className="font-bold text-slate-900 dark:text-white text-lg">{pyq.title}</p>
                      <div className="flex items-center gap-3 mt-1 text-sm">
                        <span className="font-bold text-indigo-500">{pyq.year}</span>
                        <a href={pyq.link} target="_blank" rel="noreferrer" className="text-slate-500 hover:text-indigo-500 truncate max-w-[200px] inline-block">{pyq.link}</a>
                      </div>
                    </div>
                    <button onClick={() => deletePyq(pyq.id)} className="p-2.5 bg-red-100 text-red-700 dark:bg-red-900/40 dark:text-red-300 rounded-xl hover:bg-red-200 transition shrink-0"><Trash2 className="w-5 h-5" /></button>
                  </div>
                ))}
                {(!appData.pyqs || appData.pyqs.length === 0) && (
                  <div className="text-center py-16 border-2 border-dashed border-slate-200 dark:border-slate-700 rounded-2xl bg-slate-50 dark:bg-slate-900/50">
                    <p className="text-slate-500 font-medium">No previous papers added yet.</p>
                  </div>
                )}
             </div>
          </div>
        </div>
      )}

    </div>
  );
}
