import React, { useState, useEffect } from 'react';
import { 
  Terminal, 
  Shield, 
  Lock, 
  Server, 
  Code, 
  Mail, 
  Github, 
  Linkedin, 
  ExternalLink, 
  ChevronRight,
  Menu,
  X,
  Cpu
} from 'lucide-react';

// --- Componentes Reutilizables ---

const CyberLogo = ({ className = "w-10 h-10 text-cyan-400" }) => (
  <svg viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" className={className}>
    {/* Escudo Exterior */}
    <path d="M12 22S4 16 4 9V5L12 2L20 5V9C20 16 12 22 12 22Z" stroke="currentColor" strokeWidth="1.5" strokeLinecap="round" strokeLinejoin="round"/>
    {/* Circuito Interior */}
    <path d="M12 7V11" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round"/>
    <circle cx="12" cy="14" r="1.5" fill="currentColor"/>
    <path d="M8.5 9H15.5" stroke="currentColor" strokeWidth="1.5" strokeLinecap="round" strokeLinejoin="round"/>
    <path d="M12 15.5V18" stroke="currentColor" strokeWidth="1.5" strokeLinecap="round" strokeLinejoin="round"/>
  </svg>
);

const SectionHeading = ({ children, number }) => (
  <div className="flex items-center gap-4 mb-12">
    <span className="text-cyan-400 font-mono text-xl">{number}.</span>
    <h2 className="text-3xl md:text-4xl font-bold text-slate-100 tracking-tight">{children}</h2>
    <div className="h-px bg-cyan-900/50 flex-grow ml-4"></div>
  </div>
);

// --- Componente Principal ---

export default function App() {
  const [isScrolled, setIsScrolled] = useState(false);
  const [mobileMenuOpen, setMobileMenuOpen] = useState(false);
  const [terminalText, setTerminalText] = useState('');
  
  const fullText = "> root@javer-sec:~# ./iniciar_portfolio.sh\n> Inicializando protocolos de seguridad...\n> Autenticación biométrica: ACEPTADA.\n> Desencriptando perfil de usuario...\n\n> BIENVENIDO, JAVER BORRUECO LORITE.\n> Especialista en Ciberseguridad y Ethical Hacking.";

  // Efecto de Terminal Typewriter
  useEffect(() => {
    let i = 0;
    const timer = setInterval(() => {
      setTerminalText(fullText.slice(0, i));
      i++;
      if (i > fullText.length) {
        clearInterval(timer);
      }
    }, 40);
    return () => clearInterval(timer);
  }, []);

  // Efecto de Scroll para el Navbar
  useEffect(() => {
    const handleScroll = () => {
      setIsScrolled(window.scrollY > 50);
    };
    window.addEventListener('scroll', handleScroll);
    return () => window.removeEventListener('scroll', handleScroll);
  }, []);

  const navLinks = [
    { name: 'Inicio', href: '#home' },
    { name: 'Sobre Mí', href: '#about' },
    { name: 'Habilidades', href: '#skills' },
    { name: 'Proyectos', href: '#projects' },
    { name: 'Contacto', href: '#contact' },
  ];

  return (
    <div className="min-h-screen bg-slate-950 text-slate-300 font-sans selection:bg-cyan-500/30 selection:text-cyan-200">
      
      {/* Patrón de fondo (Grid Cibernético) */}
      <div className="fixed inset-0 z-0 pointer-events-none" 
           style={{
             backgroundImage: 'linear-gradient(rgba(6, 182, 212, 0.03) 1px, transparent 1px), linear-gradient(90deg, rgba(6, 182, 212, 0.03) 1px, transparent 1px)',
             backgroundSize: '30px 30px'
           }}>
      </div>
      
      {/* Resplandor ambiental de fondo */}
      <div className="fixed top-[-10%] left-[-10%] w-[40%] h-[40%] rounded-full bg-cyan-900/20 blur-[120px] pointer-events-none z-0"></div>
      <div className="fixed bottom-[-10%] right-[-10%] w-[40%] h-[40%] rounded-full bg-cyan-800/10 blur-[120px] pointer-events-none z-0"></div>

      {/* --- NAVBAR --- */}
      <header className={`fixed top-0 w-full z-50 transition-all duration-300 border-b ${isScrolled ? 'bg-slate-950/80 backdrop-blur-md border-cyan-900/50 py-3 shadow-[0_4px_30px_rgba(6,182,212,0.1)]' : 'bg-transparent border-transparent py-5'}`}>
        <div className="max-w-6xl mx-auto px-6 flex justify-between items-center">
          {/* Logo y Nombre */}
          <a href="#home" className="flex items-center gap-3 group">
            <div className="relative">
              <div className="absolute inset-0 bg-cyan-400 blur-md opacity-0 group-hover:opacity-40 transition-opacity duration-300"></div>
              <CyberLogo className="w-8 h-8 md:w-10 md:h-10 text-cyan-400 relative z-10" />
            </div>
            <div className="flex flex-col">
              <span className="text-lg md:text-xl font-bold text-slate-100 tracking-wider group-hover:text-cyan-50 transition-colors">
                Javer Borrueco Lorite
              </span>
              <span className="text-xs font-mono text-cyan-500 uppercase tracking-widest">
                Cybersecurity Portfolio
              </span>
            </div>
          </a>

          {/* Nav Desktop */}
          <nav className="hidden md:flex gap-8 items-center">
            {navLinks.map((link, idx) => (
              <a key={idx} href={link.href} className="text-sm font-mono text-slate-400 hover:text-cyan-400 transition-colors flex items-center gap-1 group">
                <span className="text-cyan-500/50 group-hover:text-cyan-400 transition-colors">0{idx + 1}.</span>
                {link.name}
              </a>
            ))}
            <a href="#contact" className="ml-4 px-5 py-2 border border-cyan-500 text-cyan-400 font-mono text-sm rounded hover:bg-cyan-500/10 hover:shadow-[0_0_15px_rgba(6,182,212,0.3)] transition-all duration-300">
              Conectar
            </a>
          </nav>

          {/* Menú Móvil Toggle */}
          <button 
            className="md:hidden text-cyan-400 p-2"
            onClick={() => setMobileMenuOpen(!mobileMenuOpen)}
          >
            {mobileMenuOpen ? <X size={28} /> : <Menu size={28} />}
          </button>
        </div>
      </header>

      {/* Menú Móvil Overlay */}
      {mobileMenuOpen && (
        <div className="fixed inset-0 z-40 bg-slate-950/95 backdrop-blur-xl flex flex-col items-center justify-center pt-20">
          <nav className="flex flex-col gap-8 items-center w-full px-6">
            {navLinks.map((link, idx) => (
              <a 
                key={idx} 
                href={link.href} 
                onClick={() => setMobileMenuOpen(false)}
                className="text-2xl font-mono text-slate-200 hover:text-cyan-400 transition-colors w-full text-center py-4 border-b border-cyan-900/30"
              >
                <span className="text-cyan-500 block text-sm mb-1">0{idx + 1}.</span>
                {link.name}
              </a>
            ))}
          </nav>
        </div>
      )}

      {/* --- CONTENIDO PRINCIPAL --- */}
      <main className="relative z-10">
        
        {/* SECCIÓN: HERO */}
        <section id="home" className="min-h-screen flex items-center justify-center pt-20 pb-12 px-6">
          <div className="max-w-4xl w-full">
            <div className="mb-6 font-mono text-cyan-400 tracking-wider">
              Sistema Asegurado. Bienvenido.
            </div>
            <h1 className="text-5xl md:text-7xl font-extrabold text-slate-100 mb-6 leading-tight">
              Protegiendo el <br className="hidden md:block" />
              <span className="text-transparent bg-clip-text bg-gradient-to-r from-cyan-400 to-blue-500">
                entorno digital.
              </span>
            </h1>
            <p className="text-slate-400 text-lg md:text-xl max-w-2xl mb-12 leading-relaxed">
              Soy Javer Borrueco Lorite, especialista en ciberseguridad enfocado en auditorías, penetration testing y la fortificación de infraestructuras críticas. Mi objetivo es identificar vulnerabilidades antes de que lo hagan las amenazas.
            </p>

            {/* Ventana de Terminal */}
            <div className="w-full max-w-2xl bg-slate-900 rounded-lg border border-cyan-900/50 overflow-hidden shadow-[0_0_30px_rgba(0,0,0,0.5)]">
              <div className="bg-slate-950 px-4 py-2 border-b border-cyan-900/50 flex items-center gap-2">
                <div className="w-3 h-3 rounded-full bg-red-500/80"></div>
                <div className="w-3 h-3 rounded-full bg-yellow-500/80"></div>
                <div className="w-3 h-3 rounded-full bg-green-500/80"></div>
                <span className="ml-2 font-mono text-xs text-slate-500">javer@kali-linux:~</span>
              </div>
              <div className="p-4 h-48 sm:h-40 overflow-hidden bg-[#0A0F1A]">
                <pre className="font-mono text-cyan-400 text-sm md:text-base whitespace-pre-wrap leading-relaxed">
                  {terminalText}
                  <span className="animate-pulse font-bold text-cyan-300">_</span>
                </pre>
              </div>
            </div>
          </div>
        </section>

        {/* SECCIÓN: SOBRE MÍ */}
        <section id="about" className="py-24 px-6 max-w-5xl mx-auto">
          <SectionHeading number="01">Sobre Mí</SectionHeading>
          <div className="grid md:grid-cols-5 gap-12 items-center">
            <div className="md:col-span-3 space-y-6 text-slate-400 text-lg leading-relaxed">
              <p>
                Hola, soy <span className="text-cyan-400 font-semibold">Javer Borrueco Lorite</span>. Mi fascinación por la seguridad informática comenzó desarmando sistemas para entender cómo funcionaban desde su núcleo. Hoy, utilizo ese conocimiento para construir defensas robustas.
              </p>
              <p>
                Me especializo en el análisis de vulnerabilidades, pruebas de penetración en aplicaciones web y redes, y la respuesta a incidentes. Creo firmemente que la mejor defensa es una ofensa bien planificada (Ethical Hacking).
              </p>
              <p>
                Actualmente, sigo formándome en tecnologías de la nube y participo activamente en plataformas como HackTheBox y TryHackMe para mantener mis habilidades afiladas frente a las amenazas emergentes.
              </p>
            </div>
            <div className="md:col-span-2 relative group">
              {/* Marco cibernético para la foto o gráfico */}
              <div className="absolute -inset-4 border-2 border-cyan-500/20 rounded-xl transform translate-x-4 translate-y-4 transition-transform group-hover:translate-x-2 group-hover:translate-y-2"></div>
              <div className="relative bg-slate-800 border border-cyan-900/50 rounded-xl aspect-square flex items-center justify-center overflow-hidden z-10 group-hover:border-cyan-500/50 transition-colors">
                 <Shield className="w-32 h-32 text-cyan-900/50 group-hover:text-cyan-400/80 transition-all duration-500" />
                 <div className="absolute inset-0 bg-gradient-to-tr from-cyan-500/10 to-transparent opacity-0 group-hover:opacity-100 transition-opacity"></div>
              </div>
            </div>
          </div>
        </section>

        {/* SECCIÓN: HABILIDADES */}
        <section id="skills" className="py-24 px-6 max-w-5xl mx-auto">
          <SectionHeading number="02">Arsenal Técnico</SectionHeading>
          
          <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
            {[
              { icon: <Terminal size={24} />, title: 'Pentesting', desc: 'Metodologías OSSTMM, OWASP. Explotación y escalada de privilegios.' },
              { icon: <Server size={24} />, title: 'Seguridad de Redes', desc: 'Análisis de tráfico (Wireshark), segmentación, configuración de Firewalls/IDS.' },
              { icon: <Lock size={24} />, title: 'Criptografía', desc: 'Implementación de protocolos seguros, análisis de algoritmos criptográficos.' },
              { icon: <Code size={24} />, title: 'Análisis de Malware', desc: 'Ingeniería inversa básica, análisis estático y dinámico en entornos aislados.' },
              { icon: <Shield size={24} />, title: 'Auditoría Web', desc: 'Detección de XSS, SQLi, CSRF y configuración de seguridad (Burp Suite, OWASP ZAP).' },
              { icon: <Cpu size={24} />, title: 'Scripting', desc: 'Automatización de tareas defensivas y ofensivas con Python y Bash.' }
            ].map((skill, idx) => (
              <div key={idx} className="bg-slate-900/50 border border-cyan-900/30 p-6 rounded-lg hover:bg-slate-800/80 hover:border-cyan-400/50 transition-all duration-300 hover:shadow-[0_0_20px_rgba(6,182,212,0.15)] group relative overflow-hidden">
                <div className="absolute top-0 right-0 w-16 h-16 bg-gradient-to-bl from-cyan-500/10 to-transparent rounded-bl-full opacity-0 group-hover:opacity-100 transition-opacity"></div>
                <div className="text-cyan-400 mb-4 bg-cyan-950/50 w-12 h-12 rounded-lg flex items-center justify-center border border-cyan-900/50 group-hover:scale-110 transition-transform">
                  {skill.icon}
                </div>
                <h3 className="text-xl font-bold text-slate-200 mb-2">{skill.title}</h3>
                <p className="text-slate-400 text-sm leading-relaxed">{skill.desc}</p>
              </div>
            ))}
          </div>

          <div className="mt-12">
            <h3 className="text-cyan-400 font-mono mb-4 text-sm uppercase tracking-wider">Herramientas & Tecnologías</h3>
            <div className="flex flex-wrap gap-3">
              {['Kali Linux', 'Burp Suite', 'Nmap', 'Metasploit', 'Wireshark', 'Python', 'Bash', 'Docker', 'AWS Security', 'Splunk'].map((tech, i) => (
                <span key={i} className="px-4 py-2 bg-slate-900 border border-slate-700 text-slate-300 text-sm font-mono rounded hover:border-cyan-400 hover:text-cyan-300 transition-colors cursor-default">
                  {tech}
                </span>
              ))}
            </div>
          </div>
        </section>

        {/* SECCIÓN: PROYECTOS */}
        <section id="projects" className="py-24 px-6 max-w-5xl mx-auto">
          <SectionHeading number="03">Misiones / Proyectos</SectionHeading>
          
          <div className="space-y-12">
            {[
              {
                title: 'Auditoría Integral de Red Corporativa',
                desc: 'Simulación de ataque (Red Teaming) en un entorno empresarial simulado. Identificación de vulnerabilidades en Active Directory y evasión de EDR básico. Generación de informe ejecutivo y técnico con mitigaciones.',
                tech: ['Active Directory', 'BloodHound', 'Cobalt Strike (Sim)', 'PowerShell'],
                type: 'Red Teaming'
              },
              {
                title: 'Herramienta de Escaneo de Subdominios (Python)',
                desc: 'Desarrollo de un script automatizado para la recolección pasiva y activa de subdominios, integrando APIs como crt.sh y Shodan, optimizando el tiempo de reconocimiento inicial en auditorías.',
                tech: ['Python3', 'OSINT', 'APIs', 'Reconnaissance'],
                type: 'Desarrollo de Herramientas',
                github: '#'
              },
              {
                title: 'Resolución de Máquinas CTF (HackTheBox)',
                desc: 'Documentación técnica (write-ups) sobre la explotación de más de 50 máquinas de nivel intermedio a avanzado. Enfoque en explotación de servicios web y escalada de privilegios en entornos Linux y Windows.',
                tech: ['CTF', 'Privilege Escalation', 'Web Exploitation', 'Linux/Windows'],
                type: 'Investigación / CTF',
                link: '#'
              }
            ].map((project, idx) => (
              <div key={idx} className="relative grid md:grid-cols-12 gap-6 items-center group">
                {/* Contenedor "Visual" del proyecto (Simulando un log o gráfico) */}
                <div className={`md:col-span-7 bg-slate-900 border border-slate-800 rounded-lg h-64 flex items-center justify-center relative overflow-hidden ${idx % 2 !== 0 ? 'md:order-2' : ''} group-hover:border-cyan-900/50 transition-colors`}>
                   <div className="absolute inset-0 bg-[url('data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjAiIGhlaWdodD0iMjAiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyI+PGNpcmNsZSBjeD0iMSIgY3k9IjEiIHI9IjEiIGZpbGw9InJnYmEoNiwgMTgyLCAyMTIsIDAuMSkiLz48L3N2Zz4=')]"></div>
                   <Terminal className="w-20 h-20 text-slate-700/50 group-hover:text-cyan-900/40 transition-colors" />
                   
                   {/* Capa de overlay aqua */}
                   <div className="absolute inset-0 bg-cyan-500/5 mix-blend-overlay group-hover:bg-cyan-400/10 transition-colors duration-500"></div>
                </div>

                {/* Contenido de texto */}
                <div className={`md:col-span-5 z-10 ${idx % 2 !== 0 ? 'md:order-1 md:text-left' : 'md:text-right'}`}>
                  <p className="font-mono text-cyan-400 text-sm mb-2">{project.type}</p>
                  <h3 className="text-2xl font-bold text-slate-200 mb-4 group-hover:text-cyan-300 transition-colors">{project.title}</h3>
                  <div className={`bg-slate-800/90 backdrop-blur-sm p-6 rounded-lg border border-slate-700/50 shadow-xl mb-4 ${idx % 2 !== 0 ? '' : 'md:-ml-12'}`}>
                    <p className="text-slate-400 text-sm leading-relaxed">{project.desc}</p>
                  </div>
                  <ul className={`flex flex-wrap gap-3 font-mono text-xs text-slate-500 mb-6 ${idx % 2 !== 0 ? 'justify-start' : 'justify-start md:justify-end'}`}>
                    {project.tech.map((t, i) => <li key={i}>{t}</li>)}
                  </ul>
                  <div className={`flex gap-4 ${idx % 2 !== 0 ? 'justify-start' : 'justify-start md:justify-end'}`}>
                    {project.github && <a href={project.github} className="text-slate-400 hover:text-cyan-400"><Github size={20}/></a>}
                    {project.link && <a href={project.link} className="text-slate-400 hover:text-cyan-400"><ExternalLink size={20}/></a>}
                  </div>
                </div>
              </div>
            ))}
          </div>
        </section>

        {/* SECCIÓN: CONTACTO */}
        <section id="contact" className="py-32 px-6 max-w-3xl mx-auto text-center">
          <p className="font-mono text-cyan-400 mb-4">04. ¿Siguiente paso?</p>
          <h2 className="text-4xl md:text-5xl font-bold text-slate-200 mb-6">Establecer Conexión Segura</h2>
          <p className="text-slate-400 mb-10 text-lg leading-relaxed">
            Actualmente estoy abierto a nuevas oportunidades, colaboraciones o proyectos freelance en el ámbito de la ciberseguridad. Si necesitas auditar tus sistemas o buscas un perfil técnico para tu equipo, mi bandeja de entrada está abierta.
          </p>
          
          <a href="mailto:contacto@ejemplo.com" className="inline-flex items-center gap-2 px-8 py-4 bg-transparent border-2 border-cyan-500 text-cyan-400 font-mono rounded hover:bg-cyan-500/10 hover:shadow-[0_0_20px_rgba(6,182,212,0.4)] transition-all duration-300 group">
            <Mail size={20} className="group-hover:-translate-y-1 transition-transform" />
            Iniciar Handshake (Enviar Email)
          </a>

          <div className="mt-20 flex justify-center gap-8">
            <a href="#" className="text-slate-500 hover:text-cyan-400 transition-colors p-2 hover:bg-cyan-900/20 rounded-full">
              <Github size={24} />
            </a>
            <a href="#" className="text-slate-500 hover:text-cyan-400 transition-colors p-2 hover:bg-cyan-900/20 rounded-full">
              <Linkedin size={24} />
            </a>
            <a href="#" className="text-slate-500 hover:text-cyan-400 transition-colors p-2 hover:bg-cyan-900/20 rounded-full" title="HackTheBox / TryHackMe">
              <Terminal size={24} />
            </a>
          </div>
        </section>

      </main>

      {/* --- FOOTER --- */}
      <footer className="border-t border-cyan-900/30 py-6 text-center z-10 relative">
        <p className="text-slate-500 font-mono text-xs sm:text-sm">
          Diseñado y desarrollado por <span className="text-cyan-500/80">Javer Borrueco Lorite</span>
        </p>
        <p className="text-slate-600 font-mono text-xs mt-2">
          &copy; {new Date().getFullYear()} - Todos los sistemas operativos protegidos.
        </p>
      </footer>

    </div>
  );
}
