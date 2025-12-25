<!--
  GitHub Profile Readme (HTML + CSS + small JS)
  - Single-file HTML that shows a 3D animated profile card
  - To use on GitHub: host this file on GitHub Pages (or Netlify) and link to it from your README.md
  - Author: generated for Tirth Ajagiya
-->
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Tirth Ajagiya — 3D GitHub Profile</title>
  <style>
    :root{
      --bg-1: #0f1724; /* deep navy */
      --bg-2: #081226; /* darker */
      --accent: #6ee7b7; /* mint */
      --accent-2: #60a5fa; /* sky */
      --glass: rgba(255,255,255,0.06);
      --glass-2: rgba(255,255,255,0.03);
      --text: #e6eef8;
      --muted: #9fb3d6;
      --card-w: 760px;
    }

    *{box-sizing:border-box}
    html,body{height:100%;margin:0;font-family:Inter,ui-sans-serif,system-ui,-apple-system,'Segoe UI',Roboto,'Helvetica Neue',Arial}
    body{
      background: radial-gradient(1200px 600px at 10% 20%, rgba(96,165,250,0.06), transparent 10%),
                  radial-gradient(1000px 500px at 90% 80%, rgba(110,231,183,0.04), transparent 10%),
                  linear-gradient(180deg,var(--bg-1),var(--bg-2));
      color:var(--text);
      -webkit-font-smoothing:antialiased;
      -moz-osx-font-smoothing:grayscale;
      display:flex;align-items:center;justify-content:center;padding:40px;
    }

    /* stage for 3D perspective */
    .stage{
      width:100%;max-width:var(--card-w);height:460px;position:relative;perspective:1400px;
      display:flex;align-items:center;justify-content:center;
    }

    /* animated floating orbs */
    .orb{
      position:absolute;border-radius:50%;filter:blur(28px);opacity:0.55;mix-blend-mode:screen;
      animation:float 8s ease-in-out infinite alternate;
    }
    .orb.o1{width:380px;height:380px;left:-10%;top:-20%;background:linear-gradient(135deg,var(--accent),transparent)}
    .orb.o2{width:260px;height:260px;right:-8%;bottom:-30%;background:linear-gradient(135deg,var(--accent-2),transparent);animation-duration:9s}

    @keyframes float{to{transform:translateY(-22px) translateX(18px) rotate(15deg)}}

    /* the 3D card */
    .card-wrap{
      width:680px;height:380px;transform-style:preserve-3d;transition:transform 700ms cubic-bezier(.2,.9,.3,1);
      transform-origin:center;display:flex;align-items:center;justify-content:center;
    }

    .card{
      --r: 14px;
      width:640px;height:340px;border-radius:20px;padding:28px;position:relative;background:linear-gradient(135deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));
      box-shadow: 0 20px 50px rgba(2,6,23,0.6);backdrop-filter:blur(8px);transform-style:preserve-3d;overflow:hidden;border:1px solid rgba(255,255,255,0.04);
      display:grid;grid-template-columns:220px 1fr;gap:20px;align-items:center;
    }

    /* subtle rotating grid inside card */
    .card::before{
      content:"";position:absolute;inset:-40%;background-image:linear-gradient(90deg, rgba(255,255,255,0.02) 1px, transparent 1px),linear-gradient(rgba(255,255,255,0.01) 1px, transparent 1px);background-size:60px 60px,60px 60px;opacity:0.3;transform:translateZ(-60px) rotateX(20deg) scale(1.3);
    }

    /* left column: avatar */
    .avatar{
      width:220px;height:220px;border-radius:16px;background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));display:flex;align-items:center;justify-content:center;flex-direction:column;gap:12px;padding:16px;position:relative;z-index:3;border:1px solid rgba(255,255,255,0.03)
    }

    .avatar .photo{
      width:112px;height:112px;border-radius:50%;display:grid;place-items:center;font-weight:700;font-size:32px;
      background:linear-gradient(135deg,var(--accent),var(--accent-2));color:#02203a;box-shadow:0 10px 30px rgba(2,6,23,0.45);transform:translateZ(60px);
    }

    .role{font-weight:600;color:var(--muted);font-size:13px;letter-spacing:0.6px}
    .name{font-size:20px;font-weight:800;color:var(--text);margin-top:6px}

    /* right column */
    .info{display:flex;flex-direction:column;gap:10px;padding-right:6px}
    .headline{font-weight:700;font-size:16px}
    .bio{color:var(--muted);line-height:1.45}

    .stack{display:flex;gap:10px;flex-wrap:wrap;margin-top:8px}
    .chip{background:var(--glass);padding:8px 12px;border-radius:999px;font-weight:600;font-size:13px;color:var(--text);border:1px solid rgba(255,255,255,0.03);backdrop-filter:blur(6px);}

    .stats{display:flex;gap:12px;margin-top:14px}
    .stat{background:var(--glass-2);padding:8px 12px;border-radius:12px;font-weight:700;font-size:13px;color:var(--muted);display:flex;flex-direction:column;align-items:flex-start}
    .stat .num{font-size:18px;color:var(--text)}

    /* floating cubes (pure CSS 3D) */
    .cubes{position:absolute;right:18px;top:14px;transform-style:preserve-3d;pointer-events:none}
    .cube{width:36px;height:36px;position:relative;transform-style:preserve-3d;transform-origin:center;opacity:0.95;}
    .cube i{position:absolute;inset:0;border-radius:6px;background:linear-gradient(180deg,rgba(255,255,255,0.02),rgba(255,255,255,0.01));backdrop-filter:blur(4px);border:1px solid rgba(255,255,255,0.03);}
    .cube.c1{transform:translateZ(40px) rotateX(30deg) rotateY(20deg);animation:spin1 9s linear infinite}
    .cube.c2{transform:translateZ(20px) translateY(-18px) translateX(-60px) rotateX(16deg) rotateY(-20deg);animation:spin2 7s linear infinite}

    @keyframes spin1{0%{transform:translateZ(40px) rotateX(0) rotateY(0)}50%{transform:translateZ(40px) rotateX(180deg) rotateY(180deg)}100%{transform:translateZ(40px) rotateX(360deg) rotateY(360deg)}}
    @keyframes spin2{0%{transform:translateZ(20px) translateY(-18px) translateX(-60px) rotateX(0) rotateY(0)}50%{transform:translateZ(20px) translateY(-18px) translateX(-60px) rotateX(180deg) rotateY(-180deg)}100%{transform:translateZ(20px) translateY(-18px) translateX(-60px) rotateX(360deg) rotateY(360deg)}}

    /* subtle CTA */
    .cta{margin-top:auto;display:flex;gap:10px;align-items:center}
    .btn{padding:10px 14px;border-radius:12px;font-weight:700;border:0;cursor:pointer;background:linear-gradient(90deg,var(--accent),var(--accent-2));color:#032133}
    .ghost{padding:10px 14px;border-radius:12px;font-weight:700;border:1px solid rgba(255,255,255,0.06);background:transparent;color:var(--muted)}

    /* responsiveness */
    @media (max-width:760px){
      .card{grid-template-columns:1fr;grid-template-rows:auto;gap:14px;height:auto;width:92%;padding:18px}
      .stage{height:auto}
      .avatar{width:100%;flex-direction:row;justify-content:flex-start;padding:10px}
      .avatar .photo{width:72px;height:72px;font-size:20px}
      .cubes{display:none}
    }

    /* reduce motion accessibility */
    @media (prefers-reduced-motion: reduce){
      .orb, .cube{animation:none}
      .card-wrap{transition:none}
    }
  </style>
</head>
<body>
  <div class="stage" id="stage">
    <div class="orb o1" aria-hidden="true"></div>
    <div class="orb o2" aria-hidden="true"></div>

    <div class="card-wrap" id="cardWrap">
      <div class="card" role="region" aria-label="Profile card">

        <div class="avatar">
          <div class="photo" aria-hidden="true">TA</div>
          <div style="text-align:left">
            <div class="name">Tirth Ajagiya</div>
            <div class="role">Aspiring Full Stack Developer • Future IT Entrepreneur</div>
          </div>
        </div>

        <div class="info">
          <div>
            <div class="headline">I build things that people use</div>
            <div class="bio">Focused on MERN stack, clean code, and problem solving. Building practical projects (LMS, Dynamic Form Builder) and preparing for placements with DSA.</div>
            <div class="stack" aria-hidden="true">
              <div class="chip">JavaScript</div>
              <div class="chip">React</div>
              <div class="chip">Node.js</div>
              <div class="chip">MongoDB</div>
              <div class="chip">SQL</div>
              <div class="chip">C</div>
            </div>

            <div class="stats">
              <div class="stat"><div class="num">250+</div><div style="opacity:.8;font-size:12px">Target LeetCode</div></div>
              <div class="stat"><div class="num">MERN</div><div style="opacity:.8;font-size:12px">Preferred Stack</div></div>
              <div class="stat"><div class="num">Rajkot</div><div style="opacity:.8;font-size:12px">Location</div></div>
            </div>
          </div>

          <div class="cta">
            <button class="btn" onclick="openLink('https://github.com/your-username')">View GitHub</button>
            <button class="ghost" onclick="openLink('mailto:your-email@example.com')">Contact</button>
          </div>
        </div>

        <div class="cubes" aria-hidden="true">
          <div class="cube c1"><i></i></div>
          <div class="cube c2"><i></i></div>
        </div>

      </div>
    </div>
  </div>

  <script>
    // small interactive parallax: tilt card with mouse and reset on leave
    (function(){
      const wrap = document.getElementById('cardWrap');
      const card = wrap.querySelector('.card');
      const stage = document.getElementById('stage');

      function limit(v, a){ return Math.max(-a, Math.min(a, v)); }

      stage.addEventListener('mousemove', (e)=>{
        const r = stage.getBoundingClientRect();
        const x = (e.clientX - r.left) / r.width - 0.5; // -0.5..0.5
        const y = (e.clientY - r.top) / r.height - 0.5;
        const rx = limit(y * 30, 30); // tilt x
        const ry = limit(-x * 30, 30); // tilt y
        wrap.style.transform = `rotateX(${rx}deg) rotateY(${ry}deg) translateZ(0)`;
        // push inner elements slightly for parallax
        card.style.transform = `translateZ(0px)`;
      });

      stage.addEventListener('mouseleave', ()=>{
        wrap.style.transform = `rotateX(0deg) rotateY(0deg)`;
        card.style.transform = `translateZ(0px)`;
      });

      // helper for buttons
      window.openLink = function(url){
        try{ window.open(url, '_blank'); }catch(e){ location.href=url }
      }
    })();
  </script>
</body>
</html>
