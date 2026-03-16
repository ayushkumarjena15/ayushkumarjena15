import React, { useState, useEffect } from 'react';
import { 
  Download, Copy, CheckCircle2, ChevronRight, ChevronLeft, 
  Github, Twitter, Linkedin, Mail, Globe, Code2, 
  LayoutDashboard, Terminal, Activity, Award, User, Settings, Sparkles 
} from 'lucide-react';

const TECH_CATEGORIES = {
  Languages: [
    { name: 'JavaScript', badge: 'javascript-%23323330.svg?style=for-the-badge&logo=javascript&logoColor=%23F7DF1E' },
    { name: 'TypeScript', badge: 'typescript-%23007ACC.svg?style=for-the-badge&logo=typescript&logoColor=white' },
    { name: 'Python', badge: 'python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54' },
    { name: 'Java', badge: 'java-%23ED8B00.svg?style=for-the-badge&logo=openjdk&logoColor=white' },
    { name: 'C++', badge: 'c++-%2300599C.svg?style=for-the-badge&logo=c%2B%2B&logoColor=white' },
  ],
  Frontend: [
    { name: 'React', badge: 'react-%2320232a.svg?style=for-the-badge&logo=react&logoColor=%2361DAFB' },
    { name: 'Next.js', badge: 'Next-black?style=for-the-badge&logo=next.js&logoColor=white' },
    { name: 'Vue.js', badge: 'vuejs-%2335495e.svg?style=for-the-badge&logo=vuedotjs&logoColor=%234FC08D' },
    { name: 'Tailwind', badge: 'tailwindcss-%2338B2AC.svg?style=for-the-badge&logo=tailwind-css&logoColor=white' },
    { name: 'HTML5', badge: 'html5-%23E34F26.svg?style=for-the-badge&logo=html5&logoColor=white' },
    { name: 'CSS3', badge: 'css3-%231572B6.svg?style=for-the-badge&logo=css3&logoColor=white' },
  ],
  Backend: [
    { name: 'Node.js', badge: 'node.js-6DA55F?style=for-the-badge&logo=node.js&logoColor=white' },
    { name: 'Express.js', badge: 'express.js-%23404d59.svg?style=for-the-badge&logo=express&logoColor=%2361DAFB' },
    { name: 'Flask', badge: 'flask-%23000.svg?style=for-the-badge&logo=flask&logoColor=white' },
    { name: 'Django', badge: 'django-%23092E20.svg?style=for-the-badge&logo=django&logoColor=white' },
  ],
  Database: [
    { name: 'MongoDB', badge: 'MongoDB-%234ea94b.svg?style=for-the-badge&logo=mongodb&logoColor=white' },
    { name: 'PostgreSQL', badge: 'postgresql-%23316192.svg?style=for-the-badge&logo=postgresql&logoColor=white' },
    { name: 'MySQL', badge: 'mysql-%2300f.svg?style=for-the-badge&logo=mysql&logoColor=white' },
    { name: 'Supabase', badge: 'Supabase-3ECF8E?style=for-the-badge&logo=supabase&logoColor=white' },
  ],
  Tools: [
    { name: 'Git', badge: 'git-%23F05033.svg?style=for-the-badge&logo=git&logoColor=white' },
    { name: 'Docker', badge: 'docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white' },
    { name: 'Kubernetes', badge: 'kubernetes-%23326ce5.svg?style=for-the-badge&logo=kubernetes&logoColor=white' },
    { name: 'AWS', badge: 'AWS-%23FF9900.svg?style=for-the-badge&logo=amazon-aws&logoColor=white' },
  ]
};

export default function ReadmeGenerator() {
  const [step, setStep] = useState(1);
  const [copied, setCopied] = useState(false);
  const [toast, setToast] = useState(null);
  
  const [data, setData] = useState({
    username: 'ayushkumarjena15',
    name: 'Ayush Kumar Jena',
    subtitle: 'Aspiring Software Engineer & AI/ML Enthusiast',
    about1: 'working on AI/ML projects and my personal portfolio',
    about2: 'to collaborate on Open Source and innovative web apps',
    about3: 'help with scaling projects and real-world AI implementations',
    about4: 'learning DSA, Machine Learning, and Backend Development',
    about5: 'Web Dev, Portfolio Building, or DSA',
    funFact: 'I love turning ideas into real projects and sharing them with the world 🌍',
    tech: ['JavaScript', 'Python', 'React', 'Node.js', 'MongoDB', 'Git'],
    socials: {
      github: 'ayushkumarjena15',
      twitter: 'AyushJena1504',
      linkedin: 'ayush-kumar-jena-b19151321',
      portfolio: 'www.ayushkumarjena.in',
      email: 'ahalyajena28@gmail.com'
    },
    features: {
      stats: true,
      streak: true,
      trophies: true,
      views: true,
      quote: true,
      typing: true
    },
    theme: 'tokyonight' // tokyonight, dark, radical, oceanic
  });

  const showToast = (msg) => {
    setToast(msg);
    setTimeout(() => setToast(null), 3000);
  };

  const handleCopy = () => {
    navigator.clipboard.writeText(generateMarkdown());
    setCopied(true);
    showToast('Markdown copied to clipboard!');
    setTimeout(() => setCopied(false), 2000);
  };

  const handleDownload = () => {
    const element = document.createElement("a");
    const file = new Blob([generateMarkdown()], {type: 'text/markdown'});
    element.href = URL.createObjectURL(file);
    element.download = "README.md";
    document.body.appendChild(element); // Required for this to work in FireFox
    element.click();
    showToast('README.md downloaded!');
  };

  const toggleTech = (techName) => {
    setData(prev => ({
      ...prev,
      tech: prev.tech.includes(techName) 
        ? prev.tech.filter(t => t !== techName)
        : [...prev.tech, techName]
    }));
  };

  const generateMarkdown = () => {
    let md = '';

    // Header
    md += `<div align="center">\n`;
    md += `  <img src="https://media.giphy.com/media/v1.Y2lkPWVjZjA1ZTQ3bTRoem00YWJ6dGJyaWtuYTBwMmN2aTZmbmw5ZThwMTVpcmx1NjdrNiZlcD12MV9naWZzX3NlYXJjaCZjdD1n/xonOzxf2M8hNu/giphy.gif" width="100%" alt="Header Anime GIF" style="border-radius: 12px; margin-bottom: 20px;">\n\n`;
    
    if (data.features.typing) {
      const parts = data.subtitle.split('&').map(p => p.trim());
      const encodedLines = [`Hi there, I'm ${data.name} 👋`, ...parts].map(encodeURIComponent).join(';');
      md += `  <h1>\n    <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=28&pause=1000&color=2E95D3&center=true&vCenter=true&random=false&width=600&lines=${encodedLines}" alt="Typing SVG" />\n  </h1>\n`;
    } else {
      md += `  <h1>Hi there, I'm ${data.name} 👋</h1>\n`;
      md += `  <p><em>${data.subtitle}</em></p>\n`;
    }

    // Socials
    md += `\n  <div>\n`;
    if (data.socials.portfolio) md += `    <a href="https://${data.socials.portfolio}" target="_blank"><img src="https://img.shields.io/badge/Portfolio-252525?style=for-the-badge&logo=Globe&logoColor=white" alt="Portfolio"></a>\n`;
    if (data.socials.linkedin) md += `    <a href="https://linkedin.com/in/${data.socials.linkedin}" target="_blank"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn"></a>\n`;
    if (data.socials.twitter) md += `    <a href="https://x.com/${data.socials.twitter}" target="_blank"><img src="https://img.shields.io/badge/Twitter-000000?style=for-the-badge&logo=x&logoColor=white" alt="X"></a>\n`;
    if (data.socials.email) md += `    <a href="mailto:${data.socials.email}" target="_blank"><img src="https://img.shields.io/badge/Email-EA4335?style=for-the-badge&logo=gmail&logoColor=white" alt="Email"></a>\n`;
    md += `  </div>\n</div>\n\n---\n\n`;

    // About & Stats
    md += `<table align="center" style="width: 100%; max-width: 900px;">\n  <tr>\n    <td width="55%" valign="top">\n      <h3>🚀 About Me</h3>\n      <ul>\n`;
    if (data.about1) md += `        <li>🔭 Currently working on <strong>${data.about1}</strong></li>\n`;
    if (data.about2) md += `        <li>🤝 Looking to collaborate on <strong>${data.about2}</strong></li>\n`;
    if (data.about3) md += `        <li>🛠️ Seeking help with <strong>${data.about3}</strong></li>\n`;
    if (data.about4) md += `        <li>🌱 Currently learning <strong>${data.about4}</strong></li>\n`;
    if (data.about5) md += `        <li>💬 Ask me about <strong>${data.about5}</strong></li>\n`;
    if (data.funFact) md += `        <li>⚡ Fun fact: <strong>${data.funFact}</strong></li>\n`;
    md += `      </ul>\n    </td>\n`;
    
    // Mini stats
    md += `    <td width="45%" valign="center" align="center">\n`;
    if (data.features.stats && data.username) {
      md += `      <img src="https://github-readme-stats.vercel.app/api?username=${data.username}&theme=${data.theme}&hide_border=true&include_all_commits=true&count_private=true&show_icons=true" alt="GitHub Stats" width="100%"/>\n`;
    }
    md += `    </td>\n  </tr>\n</table>\n\n---\n\n`;

    // Tech Stack
    if (data.tech.length > 0) {
      md += `<h2 align="center">💻 Tech Stack & Tools</h2>\n\n<div align="center">\n`;
      Object.keys(TECH_CATEGORIES).forEach(category => {
        const categoryTechs = TECH_CATEGORIES[category].filter(t => data.tech.includes(t.name));
        if (categoryTechs.length > 0) {
          categoryTechs.forEach(t => {
            md += `  <img src="https://img.shields.io/badge/${t.badge}" alt="${t.name}" />\n`;
          });
          md += `  <br>\n`;
        }
      });
      md += `</div>\n\n---\n\n`;
    }

    // Extended Stats
    md += `<h2 align="center">📈 Coding Activity & Stats</h2>\n\n<div align="center">\n`;
    if (data.username) {
      md += `  <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=${data.username}&theme=${data.theme}&hide_border=true&include_all_commits=true&count_private=true&layout=compact" alt="Top Languages" />\n`;
      if (data.features.streak) {
        md += `  <img src="https://nirzak-streak-stats.vercel.app/?user=${data.username}&theme=${data.theme}&hide_border=true" alt="GitHub Streak" />\n`;
      }
    }
    md += `</div>\n\n<br>\n\n`;

    if (data.features.trophies && data.username) {
      md += `<div align="center">\n  <img src="https://github-profile-trophy.vercel.app/?username=${data.username}&theme=${data.theme}&no-frame=true&no-bg=true&margin-w=4" alt="GitHub Trophies" />\n</div>\n\n---\n\n`;
    }

    // Footer
    md += `<div align="center">\n`;
    if (data.features.quote) {
      md += `  <img src="https://quotes-github-readme.vercel.app/api?type=horizontal&theme=${data.theme}" alt="Random Dev Quote" />\n  <br><br>\n`;
    }
    if (data.features.views && data.username) {
      md += `  <img src="https://visitcount.itsvg.in/api?id=${data.username}&icon=0&color=0" alt="Profile Views" />\n`;
    }
    md += `</div>\n`;

    return md;
  };

  const steps = [
    { num: 1, title: 'Identity', icon: <User className="w-5 h-5" /> },
    { num: 2, title: 'About Me', icon: <Terminal className="w-5 h-5" /> },
    { num: 3, title: 'Tech Stack', icon: <Code2 className="w-5 h-5" /> },
    { num: 4, title: 'Add-ons', icon: <Sparkles className="w-5 h-5" /> },
  ];

  const handleInputChange = (e, section = null) => {
    const { name, value, type, checked } = e.target;
    if (section) {
      setData(prev => ({ ...prev, [section]: { ...prev[section], [name]: type === 'checkbox' ? checked : value } }));
    } else {
      setData(prev => ({ ...prev, [name]: type === 'checkbox' ? checked : value }));
    }
  };

  return (
    <div className="min-h-screen bg-[#0d1117] text-white font-sans selection:bg-blue-500/30 overflow-hidden relative font-['Inter',sans-serif]">
      {/* Background Orbs */}
      <div className="absolute top-[-10%] left-[-10%] w-[40%] h-[40%] bg-blue-600/20 blur-[120px] rounded-full mix-blend-screen pointer-events-none"></div>
      <div className="absolute bottom-[-10%] right-[-10%] w-[40%] h-[40%] bg-purple-600/20 blur-[120px] rounded-full mix-blend-screen pointer-events-none"></div>

      {/* Header */}
      <header className="fixed top-0 w-full z-50 backdrop-blur-md bg-[#0d1117]/80 border-b border-white/10 px-6 py-4 flex justify-between items-center shadow-lg">
        <div className="flex items-center gap-3">
          <div className="bg-gradient-to-tr from-blue-500 to-purple-500 p-2 rounded-xl shadow-lg shadow-purple-500/20">
            <LayoutDashboard className="w-6 h-6 text-white" />
          </div>
          <div>
            <h1 className="text-xl font-bold bg-clip-text text-transparent bg-gradient-to-r from-blue-400 to-purple-400">
              ProfileGen PRO
            </h1>
            <p className="text-xs text-slate-400 font-medium tracking-wide border border-slate-700 w-fit px-2 py-0.5 rounded-full mt-1">SaaS Edition</p>
          </div>
        </div>
        
        <div className="flex items-center gap-4">
          <button 
            onClick={handleCopy}
            className="flex items-center gap-2 px-4 py-2 rounded-lg bg-white/5 hover:bg-white/10 border border-white/10 transition-all active:scale-95 text-sm font-medium"
          >
            {copied ? <CheckCircle2 className="w-4 h-4 text-green-400" /> : <Copy className="w-4 h-4" />}
            {copied ? 'Copied' : 'Copy Code'}
          </button>
          <button 
            onClick={handleDownload}
            className="flex items-center gap-2 px-5 py-2 rounded-lg bg-gradient-to-r from-blue-600 to-purple-600 hover:from-blue-500 hover:to-purple-500 transition-all shadow-lg shadow-blue-500/25 border border-white/10 active:scale-95 text-sm font-medium font-semibold text-white"
          >
            <Download className="w-4 h-4" /> Export .MD
          </button>
        </div>
      </header>

      {/* Main Layout */}
      <main className="pt-24 px-6 pb-6 flex h-screen max-w-[1800px] mx-auto gap-6 relative z-10">
        
        {/* Editor Panel (Left) */}
        <div className="w-1/2 flex flex-col h-full bg-[#161b22]/60 backdrop-blur-xl border border-white/10 rounded-2xl shadow-2xl shadow-black/50 overflow-hidden relative">
          
          {/* Progress Tracker */}
          <div className="flex items-center justify-between px-8 py-5 border-b border-white/10 bg-white/5">
            {steps.map((s, i) => (
              <div key={s.num} className="flex items-center gap-3 relative z-10 cursor-pointer group" onClick={() => setStep(s.num)}>
                <div className={\`w-10 h-10 rounded-full flex items-center justify-center transition-all duration-300 shadow-lg \${step === s.num ? 'bg-gradient-to-tr from-blue-500 to-purple-500 text-white shadow-purple-500/40 ring-2 ring-white/20' : step > s.num ? 'bg-green-500/20 text-green-400 border border-green-500/30' : 'bg-[#0d1117] text-slate-400 border border-slate-700 group-hover:border-slate-500'}\`}>
                  {step > s.num ? <CheckCircle2 className="w-5 h-5" /> : s.icon}
                </div>
                <div className="hidden xl:block">
                  <p className={\`text-xs font-semibold tracking-wider uppercase \${step === s.num ? 'text-blue-400' : 'text-slate-500'}\`}>Step {s.num}</p>
                  <p className={\`text-sm font-medium \${step === s.num ? 'text-white' : 'text-slate-400'}\`}>{s.title}</p>
                </div>
              </div>
            ))}
          </div>

          {/* Form Area */}
          <div className="flex-1 overflow-y-auto p-8 custom-scrollbar">
            
            {/* Step 1: Identity */}
            <div className={\`transition-all duration-500 \${step === 1 ? 'opacity-100 translate-x-0 cursor-auto pointer-events-auto' : 'opacity-0 -translate-x-10 absolute pointer-events-none'}\`}>
              <h2 className="text-2xl font-bold mb-6 flex items-center gap-3"><User className="text-blue-400" /> Personal Identity</h2>
              
              <div className="space-y-6">
                <div>
                  <label className="block text-sm font-medium text-slate-300 mb-2">GitHub Username</label>
                  <input type="text" name="username" value={data.username} onChange={e => handleInputChange(e)} className="w-full bg-[#0d1117] border border-slate-700 rounded-lg px-4 py-3 text-white focus:outline-none focus:border-blue-500 focus:ring-1 focus:ring-blue-500 transition-all" placeholder="octocat" />
                </div>
                <div className="grid grid-cols-2 gap-4">
                  <div>
                    <label className="block text-sm font-medium text-slate-300 mb-2">Display Name</label>
                    <input type="text" name="name" value={data.name} onChange={e => handleInputChange(e)} className="w-full bg-[#0d1117] border border-slate-700 rounded-lg px-4 py-3 text-white focus:outline-none focus:border-blue-500 focus:ring-1 focus:ring-blue-500 transition-all" />
                  </div>
                  <div>
                    <label className="block text-sm font-medium text-slate-300 mb-2">Headline/Tagline</label>
                    <input type="text" name="subtitle" value={data.subtitle} onChange={e => handleInputChange(e)} className="w-full bg-[#0d1117] border border-slate-700 rounded-lg px-4 py-3 text-white focus:outline-none focus:border-blue-500 focus:ring-1 focus:ring-blue-500 transition-all" />
                  </div>
                </div>

                <div className="pt-4 border-t border-slate-800">
                  <h3 className="text-lg font-semibold mb-4 text-slate-200">Social Links</h3>
                  <div className="grid grid-cols-2 gap-4">
                    {Object.entries({
                      portfolio: { label: 'Portfolio URL', icon: <Globe className="w-4 h-4" />},
                      linkedin: { label: 'LinkedIn Username', icon: <Linkedin className="w-4 h-4" />},
                      twitter: { label: 'X/Twitter Handle', icon: <Twitter className="w-4 h-4" />},
                      email: { label: 'Email Address', icon: <Mail className="w-4 h-4" />}
                    }).map(([key, info]) => (
                      <div key={key}>
                        <label className="flex items-center gap-2 text-sm font-medium text-slate-400 mb-2">{info.icon} {info.label}</label>
                        <input type="text" name={key} value={data.socials[key]} onChange={e => handleInputChange(e, 'socials')} className="w-full bg-[#0d1117] border border-slate-700 rounded-lg px-4 py-2.5 text-white focus:outline-none focus:border-blue-500 focus:ring-1 focus:ring-blue-500 transition-all text-sm" />
                      </div>
                    ))}
                  </div>
                </div>
              </div>
            </div>

            {/* Step 2: About Me */}
            <div className={\`transition-all duration-500 \${step === 2 ? 'opacity-100 translate-x-0 cursor-auto pointer-events-auto' : 'opacity-0 -translate-x-10 absolute pointer-events-none'}\`}>
              <h2 className="text-2xl font-bold mb-6 flex items-center gap-3"><Terminal className="text-blue-400" /> About Me Prompts</h2>
              <div className="space-y-4">
                {[
                  { id: 'about1', emoji: '🔭', text: 'I’m currently working on...' },
                  { id: 'about2', emoji: '🤝', text: 'I’m looking to collaborate on...' },
                  { id: 'about3', emoji: '🛠️', text: 'I’m looking for help with...' },
                  { id: 'about4', emoji: '🌱', text: 'I’m currently learning...' },
                  { id: 'about5', emoji: '💬', text: 'Ask me about...' },
                  { id: 'funFact', emoji: '⚡', text: 'Fun fact...' }
                ].map(item => (
                  <div key={item.id} className="flex items-start gap-4 p-4 rounded-xl bg-[#0d1117]/50 border border-slate-800 focus-within:border-blue-500/50 focus-within:bg-[#0d1117] transition-all">
                    <span className="text-xl mt-1 bg-slate-800 w-10 h-10 flex items-center justify-center rounded-lg shadow-inner">{item.emoji}</span>
                    <div className="flex-1">
                      <label className="block text-xs font-semibold text-slate-400 uppercase tracking-wider mb-1">{item.text}</label>
                      <input type="text" name={item.id} value={data[item.id]} onChange={handleInputChange} className="w-full bg-transparent border-none p-0 text-white focus:outline-none focus:ring-0 text-sm placeholder-slate-600 font-medium" placeholder="Leave empty to hide..." />
                    </div>
                  </div>
                ))}
              </div>
            </div>

            {/* Step 3: Tech Stack */}
            <div className={\`transition-all duration-500 \${step === 3 ? 'opacity-100 translate-x-0 cursor-auto pointer-events-auto' : 'opacity-0 -translate-x-10 absolute pointer-events-none'}\`}>
              <div className="flex items-center justify-between mb-6">
                <h2 className="text-2xl font-bold flex items-center gap-3"><Code2 className="text-blue-400" /> Tech Arsenal</h2>
                <div className="bg-blue-500/20 text-blue-400 text-xs font-bold px-3 py-1 rounded-full border border-blue-500/30">
                  {data.tech.length} selected
                </div>
              </div>
              
              <div className="space-y-8">
                {Object.entries(TECH_CATEGORIES).map(([category, items]) => (
                  <div key={category}>
                    <h3 className="text-sm font-semibold text-slate-400 tracking-wider uppercase mb-4 border-b border-slate-800 pb-2">{category}</h3>
                    <div className="flex flex-wrap gap-3">
                      {items.map(tech => {
                        const isSelected = data.tech.includes(tech.name);
                        return (
                          <button
                            key={tech.name}
                            onClick={() => toggleTech(tech.name)}
                            className={\`px-4 py-2 rounded-xl text-sm font-medium transition-all duration-300 flex items-center gap-2 border \${isSelected ? 'bg-gradient-to-tr from-blue-600 to-purple-600 border-white/20 shadow-lg shadow-purple-500/20 scale-105 text-white' : 'bg-[#0d1117] border-slate-700 text-slate-300 hover:border-slate-500 hover:bg-slate-800'}\`}
                          >
                            {tech.name}
                          </button>
                        );
                      })}
                    </div>
                  </div>
                ))}
              </div>
            </div>

            {/* Step 4: Add-ons */}
            <div className={\`transition-all duration-500 \${step === 4 ? 'opacity-100 translate-x-0 cursor-auto pointer-events-auto' : 'opacity-0 -translate-x-10 absolute pointer-events-none'}\`}>
              <h2 className="text-2xl font-bold mb-6 flex items-center gap-3"><Sparkles className="text-blue-400" /> Extras & Widgets</h2>
              
              <div className="mb-8">
                <label className="block text-sm font-medium text-slate-300 mb-3">Card Theme Style</label>
                <div className="grid grid-cols-2 md:grid-cols-4 gap-3">
                  {['tokyonight', 'dark', 'radical', 'oceanic'].map(t => (
                    <button 
                      key={t}
                      onClick={() => setData(prev => ({...prev, theme: t}))}
                      className={\`py-3 px-4 rounded-xl text-sm font-medium border capitalize transition-all \${data.theme === t ? 'bg-blue-500/20 border-blue-500 text-blue-400 ring-2 ring-blue-500/30' : 'bg-[#0d1117] border-slate-700 text-slate-400 hover:bg-slate-800'}\`}
                    >
                      {t}
                    </button>
                  ))}
                </div>
              </div>

              <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
                {[
                  { id: 'stats', title: 'GitHub Stats Card', desc: 'Shows total stars, commits, PRs' },
                  { id: 'streak', title: 'Streak Card', desc: 'Displays current commit streak' },
                  { id: 'trophies', title: 'Profile Trophies', desc: 'Gamified achievement trophies' },
                  { id: 'typing', title: 'Animated Typing Headline', desc: 'Replaces static text with SVG typing' },
                  { id: 'quote', title: 'Dev Quote Generator', desc: 'Random programming quote' },
                  { id: 'views', title: 'Profile View Counter', desc: 'Counts unique profile visitors' }
                ].map(feature => (
                  <label key={feature.id} className={\`relative flex items-center justify-between p-4 rounded-xl border cursor-pointer transition-all \${data.features[feature.id] ? 'bg-blue-500/10 border-blue-500/50' : 'bg-[#0d1117] border-slate-800 hover:border-slate-600'}\`}>
                    <div>
                      <p className={\`text-sm font-bold \${data.features[feature.id] ? 'text-blue-400' : 'text-slate-300'}\`}>{feature.title}</p>
                      <p className="text-xs text-slate-500 mt-1">{feature.desc}</p>
                    </div>
                    <div className={\`w-10 h-6 rounded-full transition-all flex items-center p-1 \${data.features[feature.id] ? 'bg-blue-500' : 'bg-slate-700'}\`}>
                      <div className={\`w-4 h-4 bg-white rounded-full shadow-md transition-all duration-300 \${data.features[feature.id] ? 'translate-x-4' : 'translate-x-0'}\`}></div>
                    </div>
                    <input type="checkbox" className="hidden" name={feature.id} checked={data.features[feature.id]} onChange={e => handleInputChange(e, 'features')} />
                  </label>
                ))}
              </div>
            </div>

          </div>

          {/* Footer Actions */}
          <div className="p-6 border-t border-white/10 bg-white/5 flex justify-between items-center backdrop-blur-md">
            <button 
              onClick={() => setStep(Math.max(1, step - 1))}
              disabled={step === 1}
              className={\`flex items-center gap-2 px-5 py-2.5 rounded-lg font-medium transition-all \${step === 1 ? 'opacity-50 cursor-not-allowed text-slate-500 bg-transparent' : 'bg-slate-800 hover:bg-slate-700 text-white shadow-md'}\`}
            >
              <ChevronLeft className="w-4 h-4" /> Previous
            </button>
            <button 
              onClick={() => step < 4 ? setStep(step + 1) : handleDownload()}
              className="flex items-center gap-2 px-6 py-2.5 rounded-lg bg-blue-600 hover:bg-blue-500 text-white font-semibold transition-all shadow-lg shadow-blue-500/30 active:scale-95 border border-blue-400/50"
            >
              {step < 4 ? <><span className="hidden sm:inline">Next Step</span> <ChevronRight className="w-4 h-4" /></> : <><Download className="w-4 h-4" /> Export README</>}
            </button>
          </div>
        </div>

        {/* Live Preview Panel (Right) */}
        <div className="w-1/2 flex flex-col h-full bg-[#0d1117] border border-white/10 rounded-2xl shadow-xl overflow-hidden relative group">
          <div className="absolute inset-0 bg-gradient-to-b from-transparent via-[#0d1117]/50 to-[#0d1117] pointer-events-none z-10 opacity-0 group-hover:opacity-100 transition-opacity duration-500"></div>
          
          <div className="flex items-center justify-between px-6 py-4 border-b border-white/10 bg-[#161b22]">
            <div className="flex items-center gap-2">
              <div className="flex gap-1.5 mr-4">
                <div className="w-3 h-3 rounded-full bg-red-500/80"></div>
                <div className="w-3 h-3 rounded-full bg-yellow-500/80"></div>
                <div className="w-3 h-3 rounded-full bg-green-500/80"></div>
              </div>
              <Activity className="w-4 h-4 text-slate-400" />
              <h3 className="font-medium text-slate-300 text-sm">Live Markdown Preview</h3>
            </div>
            <div className="text-xs text-slate-500 bg-white/5 px-2 py-1 rounded border border-white/10">Read Only</div>
          </div>
          
          <div className="flex-1 overflow-y-auto bg-[#0d1117] custom-scrollbar p-8">
            <div className="prose prose-invert max-w-none hover:shadow-[0_0_30px_rgba(59,130,246,0.1)] transition-shadow duration-500 rounded-xl">
              {/* Fake Markdown Rendering to look like GitHub */}
              <div dangerouslySetInnerHTML={{ __html: generateMarkdown() }} className="markdown-body" />
            </div>
          </div>
        </div>
      </main>

      {/* Toast Notification */}
      <div className={\`fixed bottom-6 right-6 px-6 py-3 rounded-lg bg-slate-800 border border-slate-700 text-white font-medium shadow-2xl flex items-center gap-3 transition-all duration-300 z-50 \${toast ? 'translate-y-0 opacity-100' : 'translate-y-10 opacity-0 pointer-events-none'}\`}>
        <CheckCircle2 className="w-5 h-5 text-green-400" />
        {toast}
      </div>

      <style dangerouslySetInnerHTML={{__html: \`
        .custom-scrollbar::-webkit-scrollbar { width: 8px; }
        .custom-scrollbar::-webkit-scrollbar-track { background: transparent; }
        .custom-scrollbar::-webkit-scrollbar-thumb { background: #30363d; border-radius: 4px; }
        .custom-scrollbar::-webkit-scrollbar-thumb:hover { background: #484f58; }
        .markdown-body img { max-width: 100%; display: inline-block; margin: 0 4px 8px 0; }
        .markdown-body h1, .markdown-body h2, .markdown-body h3 { border-bottom: 1px solid #21262d; padding-bottom: 0.3em; margin-top: 24px; margin-bottom: 16px; font-weight: 600; line-height: 1.25; }
        .markdown-body ul { list-style-type: disc; padding-left: 2em; margin-bottom: 16px; }
        .markdown-body li { margin-bottom: 0.25em; line-height: 1.5; color: #c9d1d9; font-size: 14px;}
        .markdown-body em { font-style: italic; color: #8b949e;}
      \`}} />
    </div>
  );
}
