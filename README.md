import { useState, useEffect, useRef, useCallback } from "react";

// \u2500\u2500\u2500 DATA \u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500
const REPOS = [
  { id: "face", emoji: "\ud83c\udfad", old: "face_recognize_attendance_system", name: "FaceIn \u00b7 Attendance System", desc: "\ud83c\udfad Smart attendance via real-time face recognition. No more proxy bunk! Built with Python & OpenCV.", tags: ["python","opencv","face-recognition","computer-vision"], lang: "Python", color: "#3572A5", stars: 1 },
  { id: "py", emoji: "\ud83d\udc0d", old: "PythonSeries_lvl1", name: "Python Zero \u2192 Hero \u00b7 Beginner Series", desc: "\ud83d\udc0d Complete Python series from absolute zero to confident coder. Great for beginners & revision alike.", tags: ["python","tutorial","beginner","learning"], lang: "Python", color: "#3572A5", stars: 0 },
  { id: "lc", emoji: "\u2694\ufe0f", old: "Leetcode", name: "LeetCode Grind \u00b7 C++ Solutions", desc: "\u2694\ufe0f My daily LeetCode battle log \u2014 auto-synced C++ solutions. DSA grind for coding interviews.", tags: ["leetcode","dsa","cpp","interview-prep"], lang: "C++", color: "#f34b7d", stars: 0 },
  { id: "dsa", emoji: "\ud83d\udcda", old: "DSA_practical_IT-SE_Sppu", name: "SPPU DSA Practicals \u00b7 IT/SE", desc: "\ud83d\udcda All DSA practicals for SPPU IT/SE Second Year. Clean C++ \u2014 save your semester!", tags: ["sppu","dsa","cpp","university"], lang: "C++", color: "#f34b7d", stars: 0 },
  { id: "oop", emoji: "\ud83c\udfd7\ufe0f", old: "OOP_practical_IT-SE_Sppu", name: "SPPU OOP Practicals \u00b7 IT/SE", desc: "\ud83c\udfd7\ufe0f OOP practicals for SPPU IT/SE. Well-structured C++ programs from the syllabus.", tags: ["sppu","oop","cpp","university"], lang: "C++", color: "#f34b7d", stars: 0 },
];

const SKILLS = ["Python","C++","Git","GitHub","OpenCV","DSA","OOP","LeetCode"];
const TYPING_LINES = [
  "Hey there! I'm Sachin \ud83d\udc4b",
  "Engineering Student \ud83c\udf93",
  "Python | C++ | DSA Enjoyer",
  "Building cool stuff one commit at a time \ud83d\ude80",
  "The name's lazy, the code is not \u26a1",
];

// \u2500\u2500\u2500 PARTICLE CANVAS \u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500
function ParticleCanvas() {
  const canvasRef = useRef(null);
  useEffect(() => {
    const canvas = canvasRef.current;
    const ctx = canvas.getContext("2d");
    let W = canvas.width = canvas.offsetWidth;
    let H = canvas.height = canvas.offsetHeight;
    const particles = Array.from({ length: 60 }, () => ({
      x: Math.random() * W, y: Math.random() * H,
      vx: (Math.random() - 0.5) * 0.4, vy: (Math.random() - 0.5) * 0.4,
      r: Math.random() * 2 + 1,
      alpha: Math.random() * 0.5 + 0.1,
    }));
    let raf;
    const draw = () => {
      ctx.clearRect(0, 0, W, H);
      particles.forEach(p => {
        p.x += p.vx; p.y += p.vy;
        if (p.x < 0) p.x = W; if (p.x > W) p.x = 0;
        if (p.y < 0) p.y = H; if (p.y > H) p.y = 0;
        ctx.beginPath();
        ctx.arc(p.x, p.y, p.r, 0, Math.PI * 2);
        ctx.fillStyle = `rgba(88,166,255,${p.alpha})`;
        ctx.fill();
      });
      particles.forEach((a, i) => particles.slice(i + 1).forEach(b => {
        const dx = a.x - b.x, dy = a.y - b.y;
        const dist = Math.sqrt(dx * dx + dy * dy);
        if (dist < 100) {
          ctx.beginPath();
          ctx.moveTo(a.x, a.y); ctx.lineTo(b.x, b.y);
          ctx.strokeStyle = `rgba(88
