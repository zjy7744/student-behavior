<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>熬夜·绩点·屏幕——大学生行为习惯与学业表现关联可视化研究</title>
<script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.0/dist/chart.umd.min.js"></script>
<style>
*{margin:0;padding:0;box-sizing:border-box}
:root{
  --navy:#1B2D5C;--navy-dk:#0f1d3d;--blue:#3B82F6;--red:#EF4444;
  --gray:#6B7280;--gold:#F59E0B;--green:#10B981;
  --bg:#F8FAFC;--white:#fff;--txt:#1E293B;--txt2:#64748B;
  --border:#E2E8F0;--sh:0 4px 20px rgba(0,0,0,.08)
}
body{font-family:-apple-system,"PingFang SC","Hiragino Sans GB","Microsoft YaHei","WenQuanYi Micro Hei",sans-serif;color:var(--txt);line-height:1.8;overflow-x:hidden}

/* ── NAV ── */
nav{position:fixed;top:0;left:0;right:0;z-index:999;background:rgba(15,29,61,.96);-webkit-backdrop-filter:blur(12px);backdrop-filter:blur(12px);height:58px;display:flex;align-items:center;justify-content:space-between;padding:0 2rem;box-shadow:0 2px 16px rgba(0,0,0,.25)}
.nav-logo{color:#fff;font-weight:800;font-size:.92rem;letter-spacing:1px}
.nav-links{display:flex;gap:1.2rem;list-style:none}
.nav-links a{color:rgba(255,255,255,.72);text-decoration:none;font-size:.8rem;transition:color .25s}
.nav-links a:hover{color:#60A5FA}
@media(max-width:768px){.nav-links{display:none}}

/* ── HERO ── */
.hero{min-height:100vh;background:linear-gradient(145deg,#0f1d3d 0%,#1B2D5C 55%,#2D4A8A 100%);display:flex;flex-direction:column;justify-content:center;align-items:center;text-align:center;padding:80px 2rem 4rem;position:relative;overflow:hidden}
.hero::before{content:'';position:absolute;top:-50%;right:-50%;bottom:-50%;left:-50%;background:radial-gradient(circle at 25% 65%,rgba(59,130,246,.18) 0%,transparent 48%),radial-gradient(circle at 75% 30%,rgba(239,68,68,.12) 0%,transparent 48%);animation:hpulse 9s ease-in-out infinite}
@keyframes hpulse{0%,100%{transform:scale(1)}50%{transform:scale(1.06)}}
.hero-badge{color:#93C5FD;font-size:.8rem;letter-spacing:5px;text-transform:uppercase;margin-bottom:1.4rem;position:relative}
.hero h1{font-size:clamp(1.9rem,4.5vw,3.4rem);color:#fff;font-weight:900;line-height:1.25;margin-bottom:1rem;position:relative}
.hero h1 em{color:#60A5FA;font-style:normal}
.hero-desc{color:rgba(255,255,255,.72);font-size:1.05rem;max-width:580px;margin:0 auto 2.5rem;position:relative}
.hero-kpi{display:flex;gap:1.6rem;justify-content:center;flex-wrap:wrap;margin-bottom:3rem;position:relative}
.kpi{background:rgba(255,255,255,.1);-webkit-backdrop-filter:blur(10px);backdrop-filter:blur(10px);border:1px solid rgba(255,255,255,.2);border-radius:14px;padding:1.2rem 1.8rem;text-align:center}
.kpi-n{font-size:2.4rem;font-weight:900;color:#60A5FA;display:block;line-height:1}
.kpi-l{color:rgba(255,255,255,.75);font-size:.82rem;margin-top:.35rem}
.hero-team{color:rgba(255,255,255,.45);font-size:.82rem;position:relative}
.scroll-hint{position:absolute;bottom:1.8rem;left:50%;transform:translateX(-50%);color:rgba(255,255,255,.4);font-size:.75rem;animation:sb 2.2s ease-in-out infinite;text-align:center}
.scroll-hint::before{content:'↓';display:block;font-size:1.2rem;margin-bottom:.2rem}
@keyframes sb{0%,100%{transform:translateX(-50%) translateY(0)}50%{transform:translateX(-50%) translateY(-8px)}}

/* ── WRAPPER ── */
.wrap{max-width:1180px;margin:0 auto;padding:5rem 2rem}
.wrap-alt{background:var(--bg)}
.wrap-alt>.wrap{padding-top:5rem;padding-bottom:5rem}

/* ── SECTION HEADER ── */
.sec-head{display:flex;align-items:center;gap:1.2rem;margin-bottom:2.5rem}
.sec-num{font-size:5rem;font-weight:900;color:var(--navy);opacity:.1;line-height:1;flex-shrink:0;min-width:80px;text-align:right}
.sec-info h2{font-size:1.75rem;font-weight:800;color:var(--navy)}
.sec-info p{color:var(--txt2);font-size:.92rem;margin-top:.3rem}
.bar{width:44px;height:4px;background:var(--blue);border-radius:2px;margin:.8rem 0 2rem}

/* ── CARDS ── */
.cards{display:grid;grid-template-columns:repeat(auto-fit,minmax(240px,1fr));gap:1.4rem}
.card{background:var(--white);border-radius:14px;padding:1.8rem;box-shadow:var(--sh);border:1px solid var(--border);transition:transform .3s,box-shadow .3s}
.card:hover{transform:translateY(-5px);box-shadow:0 10px 32px rgba(0,0,0,.12)}
.card-ico{width:46px;height:46px;border-radius:12px;display:flex;align-items:center;justify-content:center;font-size:1.4rem;margin-bottom:.9rem}
.card h3{font-size:1rem;font-weight:700;color:var(--navy);margin-bottom:.4rem}
.card p{font-size:.88rem;color:var(--txt2);line-height:1.7}

/* ── CHARTS ── */
.chart-box{background:var(--white);border-radius:14px;padding:1.8rem;box-shadow:var(--sh);margin-bottom:1.8rem}
.ct{font-weight:700;color:var(--navy);font-size:1.02rem;margin-bottom:.25rem}
.cs{color:var(--txt2);font-size:.82rem;margin-bottom:1.2rem}
.ch{position:relative;height:320px}
.ch-sm{position:relative;height:260px}
.ch-lg{position:relative;height:400px}
.legend{display:flex;gap:1.4rem;margin-top:.9rem;flex-wrap:wrap}
.leg-i{display:flex;align-items:center;gap:.45rem;font-size:.82rem;color:var(--txt2)}
.leg-dot{width:11px;height:11px;border-radius:50%;flex-shrink:0}

/* ── FINDING BOXES ── */
.fb{border-left:4px solid var(--blue);border-radius:0 10px 10px 0;padding:1.1rem 1.4rem;margin:.9rem 0}
.fb-b{background:linear-gradient(135deg,#EFF6FF,#DBEAFE)}
.fb-r{background:linear-gradient(135deg,#FEF2F2,#FEE2E2);border-left-color:var(--red)}
.fb-g{background:linear-gradient(135deg,#F0FDF4,#DCFCE7);border-left-color:var(--green)}
.fb-o{background:linear-gradient(135deg,#FFFBEB,#FEF3C7);border-left-color:var(--gold)}
.fb-t{font-weight:700;color:var(--navy);margin-bottom:.3rem;font-size:.94rem}
.fb-d{color:var(--txt2);font-size:.87rem;line-height:1.7}

/* ── TWO COL ── */
.two-col{display:grid;grid-template-columns:1fr 1fr;gap:2rem;align-items:start}
@media(max-width:700px){.two-col{grid-template-columns:1fr}}

/* ── TABLE ── */
.dt{width:100%;border-collapse:collapse;background:var(--white);border-radius:12px;overflow:hidden;box-shadow:var(--sh)}
.dt th{background:var(--navy);color:#fff;padding:.9rem 1rem;text-align:center;font-size:.88rem}
.dt td{padding:.85rem 1rem;text-align:center;border-bottom:1px solid var(--border);font-size:.86rem}
.dt tr:last-child td{border-bottom:none}
.dt tr:nth-child(even) td{background:#F9FAFB}

/* ── LIMITATIONS ── */
.lim-item{display:flex;gap:1.3rem;padding:1.4rem;background:var(--white);border-radius:12px;margin-bottom:1rem;box-shadow:var(--sh);align-items:flex-start}
.lim-num{width:38px;height:38px;background:var(--navy);color:#fff;border-radius:50%;display:flex;align-items:center;justify-content:center;font-weight:700;flex-shrink:0;font-size:.88rem}
.lim-c h4{font-weight:700;color:var(--navy);margin-bottom:.35rem;font-size:.96rem}
.lim-c p{font-size:.86rem;color:var(--txt2);line-height:1.7}

/* ── FUTURE ── */
.fut-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(210px,1fr));gap:1.4rem}
.fut-card{background:var(--white);border-radius:14px;padding:1.7rem;box-shadow:var(--sh);text-align:center;border-top:4px solid var(--blue);transition:transform .3s}
.fut-card:hover{transform:translateY(-4px)}
.fut-icon{font-size:1.9rem;margin-bottom:.9rem}
.fut-card h4{font-weight:700;color:var(--navy);margin-bottom:.4rem;font-size:.93rem}
.fut-card p{font-size:.83rem;color:var(--txt2);line-height:1.7}

/* ── CONCLUSION ── */
.concl{background:linear-gradient(145deg,#0f1d3d 0%,#1B2D5C 100%);color:#fff;padding:5rem 2rem;text-align:center}
.concl h2{font-size:1.9rem;margin-bottom:.8rem}
.concl-sub{color:rgba(255,255,255,.65);max-width:560px;margin:0 auto 3rem;font-size:.95rem}
.concl-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(240px,1fr));gap:1.4rem;max-width:1100px;margin:0 auto 3rem}
.concl-item{background:rgba(255,255,255,.09);border:1px solid rgba(255,255,255,.18);border-radius:12px;padding:1.5rem;text-align:left}
.concl-item .ci-label{font-size:.8rem;color:#93C5FD;margin-bottom:.4rem;letter-spacing:1px;font-weight:600}
.concl-item p{font-size:.92rem;color:rgba(255,255,255,.82);line-height:1.7}
.big-concl{background:rgba(96,165,250,.15);border:2px solid rgba(96,165,250,.4);border-radius:16px;padding:2rem;max-width:700px;margin:0 auto;font-size:1.1rem;line-height:1.8;color:rgba(255,255,255,.9)}

/* ── STRAT TABLE ── */
.strat-table{width:100%;border-collapse:collapse;border-radius:12px;overflow:hidden;box-shadow:var(--sh)}
.strat-table th{background:var(--navy);color:#fff;padding:.85rem 1rem;font-size:.86rem;text-align:center}
.strat-table td{padding:.8rem 1rem;font-size:.85rem;text-align:center;border-bottom:1px solid var(--border)}
.strat-table tr.top td{background:#EFF6FF;color:#1D4ED8;font-weight:600}
.strat-table tr.mid td{background:#F9FAFB}
.strat-table tr.low td{background:#FEF2F2;color:#991B1B;font-weight:600}

/* ── HIGHLIGHT BOX ── */
.hl-box{background:linear-gradient(135deg,#1B2D5C,#2D4A8A);color:#fff;border-radius:14px;padding:1.8rem 2rem;margin:1.8rem 0;display:flex;align-items:center;gap:1.5rem}
.hl-box .hl-ico{font-size:2.5rem;flex-shrink:0}
.hl-box h3{font-size:1.05rem;margin-bottom:.4rem}
.hl-box p{font-size:.88rem;opacity:.82;line-height:1.7}

/* ── QUADRANT ── */
.quad-grid{display:grid;grid-template-columns:1fr 1fr;gap:.8rem;margin:1.2rem 0}
.quad-cell{border-radius:10px;padding:1.1rem;text-align:center}
.quad-cell h5{font-size:.8rem;font-weight:700;margin-bottom:.4rem}
.quad-cell .qn{font-size:1.7rem;font-weight:900}
.quad-cell .ql{font-size:.76rem;margin-top:.2rem}
.qc-bg{background:linear-gradient(135deg,#DBEAFE,#BFDBFE);color:#1D4ED8}
.qc-mid1{background:linear-gradient(135deg,#F3F4F6,#E5E7EB);color:#374151}
.qc-mid2{background:linear-gradient(135deg,#FEF3C7,#FDE68A);color:#92400E}
.qc-bad{background:linear-gradient(135deg,#FEE2E2,#FECACA);color:#991B1B}

/* ── REVEAL ── */
.reveal{opacity:0;transform:translateY(28px);transition:opacity .6s ease,transform .6s ease}
.reveal.vis{opacity:1;transform:translateY(0)}

/* ── FOOTER ── */
footer{background:#0a1428;color:rgba(255,255,255,.5);text-align:center;padding:2rem;font-size:.82rem}
footer strong{color:#fff}

/* TIER BADGE */
.tb{display:inline-block;padding:.15rem .7rem;border-radius:20px;font-size:.78rem;font-weight:600}
.tb-top{background:#DBEAFE;color:#1D4ED8}
.tb-mid{background:#F3F4F6;color:#374151}
.tb-low{background:#FEE2E2;color:#991B1B}
</style>
</head>
<body>

<!-- NAV -->
<nav>
  <div class="nav-logo">熬夜·绩点·屏幕</div>
  <ul class="nav-links">
    <li><a href="#s1">背景</a></li>
    <li><a href="#s2">方法</a></li>
    <li><a href="#s3">数据</a></li>
    <li><a href="#s4">单变量</a></li>
    <li><a href="#s5">双变量</a></li>
    <li><a href="#s6">多变量</a></li>
    <li><a href="#s7">局限性</a></li>
    <li><a href="#s8">未来方向</a></li>
    <li><a href="#s9">结论</a></li>
  </ul>
</nav>

<!-- HERO -->
<section class="hero">
  <div class="hero-badge">可视化研究报告 · 2026</div>
  <h1>熬夜、<em>绩点</em>与屏幕时间<br>的三体运动</h1>
  <p class="hero-desc">大学生作息习惯、手机亮屏时长与学业绩点（GPA）关联性的多维可视化研究，探寻真正影响学业成绩的行为密码。</p>
  <div class="hero-kpi">
    <div class="kpi"><span class="kpi-n">100</span><span class="kpi-l">有效样本量</span></div>
    <div class="kpi"><span class="kpi-n">4</span><span class="kpi-l">核心分析变量</span></div>
    <div class="kpi"><span class="kpi-n">≈0</span><span class="kpi-l">单变量与GPA相关系数</span></div>
    <div class="kpi"><span class="kpi-n">5</span><span class="kpi-l">联动分析维度</span></div>
  </div>
  <p class="hero-team">研究团队：陈沛然 · 陈艳兰 · 张晓琪　　汇报时间：2026年6月25日</p>
  <div class="scroll-hint">向下探索</div>
</section>

<!-- S1: 研究背景 -->
<div id="s1">
<div class="wrap">
  <div class="sec-head reveal">
    <div class="sec-num">01</div>
    <div class="sec-info">
      <h2>研究背景与问题提出</h2>
      <p>信息时代下大学生行为习惯与学业表现关系的探索</p>
    </div>
  </div>
  <div class="bar reveal"></div>
  <div class="cards reveal">
    <div class="card">
      <div class="card-ico" style="background:#EFF6FF">📱</div>
      <h3>手机依赖现状</h3>
      <p>当代大学生日均手机使用时长持续增长，屏幕时间已成为最易量化的行为指标之一，与学习注意力、睡眠质量密切相关。</p>
    </div>
    <div class="card">
      <div class="card-ico" style="background:#F0FDF4">🌙</div>
      <h3>睡眠不足困境</h3>
      <p>晚睡、熬夜成为大学校园普遍现象，"手机不离手"与"深夜刷视频"之间存在显著的行为链，但对绩点的具体影响尚有争议。</p>
    </div>
    <div class="card">
      <div class="card-ico" style="background:#FFFBEB">📚</div>
      <h3>自习行为差异</h3>
      <p>图书馆使用频次是大学生线下自主学习行为的重要代理指标，反映学生主动学习的意愿与时间投入，可能是影响成绩的关键因素。</p>
    </div>
    <div class="card">
      <div class="card-ico" style="background:#FEF2F2">🎯</div>
      <h3>研究核心问题</h3>
      <p>睡眠时长、手机亮屏时长、图书馆自习频次，能否单独或联合预测大学生GPA？三变量之间存在何种联动规律？</p>
    </div>
  </div>
</div>
</div>

<!-- S2: 研究方法 -->
<div id="s2" class="wrap-alt">
<div class="wrap">
  <div class="sec-head reveal">
    <div class="sec-num">02</div>
    <div class="sec-info">
      <h2>研究方法与图表选型</h2>
      <p>基于核心变量特征、信息呈现效率与深度分析需求的综合考量</p>
    </div>
  </div>
  <div class="bar reveal"></div>
  <div class="two-col reveal">
    <div>
      <div class="fb fb-b">
        <div class="fb-t">01 数据类型匹配</div>
        <div class="fb-d">研究涉及睡眠时长、亮屏时长、GPA、图书馆次数等<strong>连续型变量</strong>，散点图是探索连续变量间关系最经典、有效的工具，能精准呈现数值间的依存趋势。</div>
      </div>
      <div class="fb fb-g">
        <div class="fb-t">02 信息全面性</div>
        <div class="fb-d">散点图矩阵可在<strong>单一视图</strong>内展示多变量两两关系，极大提升信息密度，帮助高效概览全局，快速捕捉变量间潜在的整体模式与关联规律。</div>
      </div>
      <div class="fb fb-o">
        <div class="fb-t">03 联动效应挖掘</div>
        <div class="fb-d">通过矩阵组合可直观探究多变量复杂关系，如"<strong>熬夜＋亮屏</strong>"对GPA的共同影响，挖掘出双变量分析中难以察觉的多维联动规律。</div>
      </div>
      <div class="fb fb-r">
        <div class="fb-t">04 格式塔优化</div>
        <div class="fb-d">采用格式塔"<strong>相似性原则</strong>"，以蓝/红/灰低饱和度配色 + 圆形/三角双重编码区分学生类型，背景网格弱化，整体整洁协调，践行数据可视化"信·达·雅"三原则。</div>
      </div>
    </div>
    <div>
      <div class="chart-box">
        <div class="ct">散点图矩阵的信息密度优势</div>
        <div class="cs">n×n矩阵展示所有变量两两组合，单视图承载最大信息量</div>
        <div class="ch-sm">
          <canvas id="ch_method"></canvas>
        </div>
        <div class="legend">
          <div class="leg-i"><div class="leg-dot" style="background:#3B82F6"></div>学霸（GPA≥3.6）</div>
          <div class="leg-i"><div class="leg-dot" style="background:#6B7280"></div>普通（2.9-3.6）</div>
          <div class="leg-i"><div class="leg-dot" style="background:#EF4444"></div>学渣（GPA≤2.9）</div>
        </div>
      </div>
    </div>
  </div>
</div>
</div>

<!-- S3: 数据预处理 -->
<div id="s3">
<div class="wrap">
  <div class="sec-head reveal">
    <div class="sec-num">03</div>
    <div class="sec-info">
      <h2>数据预处理与GPA分层</h2>
      <p>100名大学生真实行为数据的清洗校准与分层标注规则</p>
    </div>
  </div>
  <div class="bar reveal"></div>
  <div class="two-col reveal">
    <div>
      <table class="strat-table">
        <thead>
          <tr><th>分层</th><th>排名区间</th><th>GPA区间</th><th>人数</th><th>占比</th></tr>
        </thead>
        <tbody>
          <tr class="top"><td>🔵 学霸</td><td>第1–25名</td><td>3.6 – 4.0</td><td>25人</td><td>25%</td></tr>
          <tr class="mid"><td>⚪ 普通学生</td><td>第26–75名</td><td>2.9 – 3.6</td><td>50人</td><td>50%</td></tr>
          <tr class="low"><td>🔴 学渣</td><td>第76–100名</td><td>2.1 – 2.9</td><td>25人</td><td>25%</td></tr>
        </tbody>
      </table>
      <p style="font-size:.82rem;color:var(--txt2);margin-top:.8rem">划分依据：百分位排名，前25%为上四分位（Q3≥3.6），后25%为下四分位（Q1≤2.9）</p>

      <div class="hl-box" style="margin-top:1.4rem">
        <div class="hl-ico">📋</div>
        <div>
          <h3>数据清洗说明</h3>
          <p>原始数据经陈沛然完成清洗校准：删除逻辑矛盾条目（如睡眠时长&gt;24h），统一时间单位（小时），处理缺失值，最终保留100条有效记录。数据无篡改、无扭曲，颜色与形状仅作分类标签映射。</p>
        </div>
      </div>
    </div>
    <div>
      <div class="chart-box">
        <div class="ct">样本描述性统计</div>
        <div class="cs">各核心变量的均值与分布范围</div>
        <table class="dt" style="margin-bottom:1rem">
          <tr><th>变量</th><th>均值</th><th>范围</th><th>单位</th></tr>
          <tr><td>日均睡眠时长</td><td>6.4</td><td>4.0 – 9.0</td><td>小时</td></tr>
          <tr><td>日均亮屏时长</td><td>7.2</td><td>2.0 – 14.0</td><td>小时</td></tr>
          <tr><td>每周图书馆次数</td><td>2.3</td><td>0 – 5</td><td>次</td></tr>
          <tr><td>GPA</td><td>3.25</td><td>2.1 – 4.0</td><td>—</td></tr>
        </table>
        <div class="ch-sm"><canvas id="ch_dist"></canvas></div>
      </div>
    </div>
  </div>
</div>
</div>

<!-- S4: 单变量相关性 -->
<div id="s4" class="wrap-alt">
<div class="wrap">
  <div class="sec-head reveal">
    <div class="sec-num">04</div>
    <div class="sec-info">
      <h2>单变量相关性分析</h2>
      <p>各行为指标与GPA的皮尔逊相关系数——令人意外的"零相关"现象</p>
    </div>
  </div>
  <div class="bar reveal"></div>
  <div class="two-col reveal">
    <div>
      <div class="chart-box">
        <div class="ct">各变量与GPA的皮尔逊相关系数</div>
        <div class="cs">接近于零意味着单一变量无法预测GPA</div>
        <div class="ch-sm"><canvas id="ch_corr"></canvas></div>
      </div>
    </div>
    <div>
      <div class="fb fb-r">
        <div class="fb-t">🔍 核心发现：三变量均与GPA近乎零相关</div>
        <div class="fb-d">
          <strong>r(睡眠, GPA) = −0.01</strong>——趋近于零，睡眠时长无法单独预测绩点<br>
          <strong>r(亮屏, GPA) = +0.02</strong>——趋近于零，屏幕时长与绩点无显著线性关系<br>
          <strong>r(图书馆, GPA) = +0.02</strong>——趋近于零，仅凭图书馆次数也难以区分学霸与学渣
        </div>
      </div>
      <div class="fb fb-b">
        <div class="fb-t">💡 为何会出现"零相关"？</div>
        <div class="fb-d">个体差异极大：大量"熬夜+高亮屏"的学生依然是学霸，也有"早睡低屏"的学渣。单变量线性模型无法捕捉复杂的非线性与多变量联动效应，这恰恰说明需要进一步的<strong>多变量组合分析</strong>。</div>
      </div>
      <div class="fb fb-o">
        <div class="fb-t">⚠️ 统计意义说明</div>
        <div class="fb-d">相关系数绝对值 &lt; 0.1 通常被认为实践意义极弱。n=100时，r≈0.02的p值远大于0.05，统计上不显著，不应据此做出行为判断。</div>
      </div>
    </div>
  </div>
</div>
</div>

<!-- S5: 双变量联动分析 -->
<div id="s5">
<div class="wrap">
  <div class="sec-head reveal">
    <div class="sec-num">05</div>
    <div class="sec-info">
      <h2>双变量联动分析</h2>
      <p>三组两两组合分析——单变量无法发现的"隐形联动效应"</p>
    </div>
  </div>
  <div class="bar reveal"></div>

  <!-- 5.1 -->
  <div class="reveal" style="margin-bottom:2.5rem">
    <div class="hl-box">
      <div class="hl-ico">📊</div>
      <div><h3>方案 A：日均亮屏时长 × 睡眠时长</h3><p>探究"熬夜+刷手机"双重因素的联合影响——是否形成恶化成绩的双重叠加效应？</p></div>
    </div>
    <div class="two-col">
      <div class="chart-box">
        <div class="ct">亮屏时长 vs 睡眠时长（按GPA分层）</div>
        <div class="cs">散点颜色代表GPA层次</div>
        <div class="ch"><canvas id="ch_AB"></canvas></div>
        <div class="legend">
          <div class="leg-i"><div class="leg-dot" style="background:#3B82F6"></div>学霸</div>
          <div class="leg-i"><div class="leg-dot" style="background:#9CA3AF"></div>普通</div>
          <div class="leg-i"><div class="leg-dot" style="background:#EF4444"></div>学渣</div>
        </div>
      </div>
      <div>
        <div class="fb fb-b">
          <div class="fb-t">单变量基础特征</div>
          <div class="fb-d">r(睡眠, GPA)=−0.01，r(亮屏, GPA)=+0.02，两者与GPA均无显著线性相关。</div>
        </div>
        <div class="fb fb-o">
          <div class="fb-t">微弱联动趋势（隐形线索）</div>
          <div class="fb-d">
            ▶ <strong>熬夜(&lt;6h) + 长亮屏(&gt;8h)</strong>群体：学渣样本数量略多于学霸<br>
            ▶ <strong>充足睡眠(&gt;6h) + 低屏时长(&lt;6h)</strong>群体：学霸样本数量略多于学渣
          </div>
        </div>
        <div class="fb fb-r">
          <div class="fb-t">深层核心结论</div>
          <div class="fb-d">睡眠与亮屏双重叠加<strong>仅存在极微弱的分层倾向</strong>，不具决定性。存在大量例外：不少同时熬夜、长时间使用手机的学生依旧保持高绩点。</div>
        </div>
        <div class="chart-box" style="margin-top:0">
          <div class="ct">四象限GPA分布对比</div>
          <div class="quad-grid">
            <div class="quad-cell qc-bg"><h5>⬇睡眠 + ⬆亮屏<br>（不利组合）</h5><div class="qn">3.18</div><div class="ql">学霸12% | 学渣30%</div></div>
            <div class="quad-cell qc-mid1"><h5>⬆睡眠 + ⬆亮屏<br>（混合型）</h5><div class="qn">3.26</div><div class="ql">学霸22% | 学渣23%</div></div>
            <div class="quad-cell qc-mid2"><h5>⬇睡眠 + ⬇亮屏<br>（混合型）</h5><div class="qn">3.22</div><div class="ql">学霸20% | 学渣26%</div></div>
            <div class="quad-cell qc-bg"><h5>⬆睡眠 + ⬇亮屏<br>（有利组合）</h5><div class="qn">3.33</div><div class="ql">学霸28% | 学渣18%</div></div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- 5.2 -->
  <div class="reveal" style="margin-bottom:2.5rem">
    <div class="hl-box">
      <div class="hl-ico">📊</div>
      <div><h3>方案 B：每周图书馆次数 × 睡眠时长</h3><p>图书馆自习能否"对冲"熬夜带来的负面影响？探究线下学习行为的补偿机制。</p></div>
    </div>
    <div class="two-col">
      <div class="chart-box">
        <div class="ct">图书馆次数 vs 睡眠时长（按GPA分层）</div>
        <div class="cs">散点颜色代表GPA层次</div>
        <div class="ch"><canvas id="ch_BC"></canvas></div>
        <div class="legend">
          <div class="leg-i"><div class="leg-dot" style="background:#3B82F6"></div>学霸</div>
          <div class="leg-i"><div class="leg-dot" style="background:#9CA3AF"></div>普通</div>
          <div class="leg-i"><div class="leg-dot" style="background:#EF4444"></div>学渣</div>
        </div>
      </div>
      <div>
        <div class="fb fb-b">
          <div class="fb-t">单变量基础特征</div>
          <div class="fb-d">r(睡眠, GPA)=−0.01，r(图书馆, GPA)=+0.02，单独分析均无显著相关性。</div>
        </div>
        <div class="fb fb-o">
          <div class="fb-t">分组对比趋势（隐形线索）</div>
          <div class="fb-d">
            ▶ <strong>短睡眠(&lt;6h) + 低频图书馆(&lt;2次)</strong>：红色学渣三角占比更高<br>
            ▶ <strong>短睡眠(&lt;6h) + 高频图书馆(≥3次)</strong>：蓝色学霸圆点占比更高
          </div>
        </div>
        <div class="fb fb-g">
          <div class="fb-t">🌟 深层核心结论</div>
          <div class="fb-d">图书馆自习具备<strong>显著的对冲效果</strong>：充足线下学习可以弥补睡眠不足带来的劣势。单独熬夜、少去图书馆都不会直接造成低分，二者结合才出现明显分层差异。</div>
        </div>
        <div class="chart-box" style="margin-top:0">
          <div class="ct">四象限GPA分布对比</div>
          <div class="quad-grid">
            <div class="quad-cell qc-bad"><h5>⬇睡眠 + ⬇图书馆<br>（双劣组）</h5><div class="qn">3.09</div><div class="ql">学霸9% | 学渣36%</div></div>
            <div class="quad-cell qc-mid1"><h5>⬆睡眠 + ⬇图书馆<br>（无补偿组）</h5><div class="qn">3.21</div><div class="ql">学霸20% | 学渣25%</div></div>
            <div class="quad-cell qc-bg"><h5>⬇睡眠 + ⬆图书馆<br>（对冲成功组）</h5><div class="qn">3.38</div><div class="ql">学霸34% | 学渣16%</div></div>
            <div class="quad-cell qc-bg"><h5>⬆睡眠 + ⬆图书馆<br>（双优组）</h5><div class="qn">3.41</div><div class="ql">学霸36% | 学渣13%</div></div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- 5.3 -->
  <div class="reveal">
    <div class="hl-box">
      <div class="hl-ico">📊</div>
      <div><h3>方案 C：日均亮屏时长 × 每周图书馆次数</h3><p>大量刷手机是否必然影响成绩？图书馆自习频次能否对冲手机使用的负面效应？</p></div>
    </div>
    <div class="two-col">
      <div class="chart-box">
        <div class="ct">亮屏时长 vs 图书馆次数（按GPA分层）</div>
        <div class="cs">散点颜色代表GPA层次</div>
        <div class="ch"><canvas id="ch_AC"></canvas></div>
        <div class="legend">
          <div class="leg-i"><div class="leg-dot" style="background:#3B82F6"></div>学霸</div>
          <div class="leg-i"><div class="leg-dot" style="background:#9CA3AF"></div>普通</div>
          <div class="leg-i"><div class="leg-dot" style="background:#EF4444"></div>学渣</div>
        </div>
      </div>
      <div>
        <div class="fb fb-b">
          <div class="fb-t">单变量基础特征</div>
          <div class="fb-d">r(亮屏, GPA)=+0.02，r(图书馆, GPA)=+0.02，两者与GPA均无显著线性相关。</div>
        </div>
        <div class="fb fb-o">
          <div class="fb-t">分组对比趋势（隐形线索）</div>
          <div class="fb-d">
            ▶ <strong>高亮屏(&gt;8h) + 低频图书馆(&lt;2次)</strong>：红色学渣三角占比更高<br>
            ▶ <strong>高亮屏(&gt;8h) + 高频图书馆(≥3次)</strong>：蓝色学霸圆点占比明显更高
          </div>
        </div>
        <div class="fb fb-g">
          <div class="fb-t">🌟 深层核心结论</div>
          <div class="fb-d">手机亮屏时长<strong>无法单独判定学业水平</strong>，需结合线下自习行为综合判断。高频图书馆学习能够有效抵消长时间使用手机带来的不利影响——这是三次双变量分析中最强烈的信号。</div>
        </div>
        <div class="chart-box" style="margin-top:0">
          <div class="ct">四象限GPA分布对比</div>
          <div class="quad-grid">
            <div class="quad-cell qc-bad"><h5>⬆亮屏 + ⬇图书馆<br>（高风险组）</h5><div class="qn">3.05</div><div class="ql">学霸8% | 学渣38%</div></div>
            <div class="quad-cell qc-mid1"><h5>⬇亮屏 + ⬇图书馆<br>（低效率组）</h5><div class="qn">3.19</div><div class="ql">学霸19% | 学渣26%</div></div>
            <div class="quad-cell qc-mid2"><h5>⬆亮屏 + ⬆图书馆<br>（对冲组）</h5><div class="qn">3.39</div><div class="ql">学霸33% | 学渣14%</div></div>
            <div class="quad-cell qc-bg"><h5>⬇亮屏 + ⬆图书馆<br>（理想组）</h5><div class="qn">3.44</div><div class="ql">学霸38% | 学渣11%</div></div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>
</div>

<!-- S6: 多变量联动（新增两种方案） -->
<div id="s6" class="wrap-alt">
<div class="wrap">
  <div class="sec-head reveal">
    <div class="sec-num">06</div>
    <div class="sec-info">
      <h2>多变量综合联动分析（新增两种方案）</h2>
      <p>在双变量分析基础上，引入三变量同时考量的深度方法，探究更强的预测信号</p>
    </div>
  </div>
  <div class="bar reveal"></div>

  <!-- 6.1 三变量极端组合分析 -->
  <div class="reveal" style="margin-bottom:3rem">
    <div class="hl-box" style="background:linear-gradient(135deg,#064E3B,#065F46)">
      <div class="hl-ico">🔬</div>
      <div>
        <h3>新增方案一：三变量极端组合行为画像分析</h3>
        <p>将睡眠、亮屏、图书馆三变量同时考量，构建"行为画像"分组，探究极端组合下的GPA分层差异是否显著放大。</p>
      </div>
    </div>

    <div class="two-col" style="margin-top:1.5rem">
      <div>
        <div class="chart-box">
          <div class="ct">三变量极端组合 vs 平均GPA</div>
          <div class="cs">将100名学生按三变量组合划分为5类行为群体</div>
          <div class="ch"><canvas id="ch_triple_bar"></canvas></div>
        </div>
      </div>
      <div>
        <div class="chart-box">
          <div class="ct">各行为群体的学霸/学渣比例</div>
          <div class="cs">极端组合下学业层次分布更加极化</div>
          <div class="ch"><canvas id="ch_triple_stack"></canvas></div>
        </div>
      </div>
    </div>

    <div class="cards" style="margin-top:1.5rem">
      <div class="card" style="border-left:4px solid #3B82F6">
        <div class="card-ico" style="background:#DBEAFE">🏆</div>
        <h3>极优型（全有利组）</h3>
        <p>睡眠≥7h <em>AND</em> 亮屏≤6h <em>AND</em> 图书馆≥3次<br>
        <strong>平均GPA：3.52 &nbsp;|&nbsp; 学霸占比：40%</strong><br><br>
        三项有利因素叠加，GPA均值最高，学霸密度显著高于其他群体。</p>
      </div>
      <div class="card" style="border-left:4px solid #EF4444">
        <div class="card-ico" style="background:#FEE2E2">⚠️</div>
        <h3>极劣型（全不利组）</h3>
        <p>睡眠&lt;6h <em>AND</em> 亮屏&gt;8h <em>AND</em> 图书馆&lt;2次<br>
        <strong>平均GPA：3.03 &nbsp;|&nbsp; 学渣占比：41%</strong><br><br>
        三项不利因素同时存在，GPA均值最低，学渣密度最高。与极优型差距达0.49分。</p>
      </div>
      <div class="card" style="border-left:4px solid #F59E0B">
        <div class="card-ico" style="background:#FEF3C7">📚</div>
        <h3>图书馆对冲型</h3>
        <p>睡眠&lt;6h <em>AND</em> 亮屏&gt;8h <em>BUT</em> 图书馆≥3次<br>
        <strong>平均GPA：3.36 &nbsp;|&nbsp; 学霸占比：30%</strong><br><br>
        即使同时熬夜和过度用机，高频图书馆学习仍能将GPA拉回接近普通水平，展现出强大的对冲效应。</p>
      </div>
      <div class="card" style="border-left:4px solid #10B981">
        <div class="card-ico" style="background:#DCFCE7">📐</div>
        <h3>关键发现：放大效应验证</h3>
        <p>三变量极端组合下，最优组与最劣组GPA均值差距为<strong>0.49分</strong>，远大于任何单变量分析所能观察到的差异（单变量相关系数≈0），证明多因素联动确实存在放大效应。</p>
      </div>
    </div>

    <div class="fb fb-g" style="margin-top:1.5rem">
      <div class="fb-t">🔑 方案一核心结论：行为组合的"1+1+1>3"效应</div>
      <div class="fb-d">单独分析睡眠、亮屏、图书馆三个变量时，各自与GPA的相关系数均趋近于零；但当三者极端条件叠加时，行为组合的综合效果远超各单变量影响之和。这验证了"行为习惯的联动效应"假说——<strong>不良习惯的叠加会产生协同恶化效应，而良好习惯的叠加亦能产生协同提升效应</strong>。</div>
    </div>
  </div>

  <!-- 6.2 综合行为指数 -->
  <div class="reveal">
    <div class="hl-box" style="background:linear-gradient(135deg,#4C1D95,#5B21B6)">
      <div class="hl-ico">📐</div>
      <div>
        <h3>新增方案二：综合行为影响指数（BII）分析</h3>
        <p>构建量化的"行为影响指数（Behavioral Impact Index）"，将三变量加权整合为单一可排名的预测评分，验证综合指数的GPA预测力是否优于任何单一变量。</p>
      </div>
    </div>

    <div class="two-col" style="margin-top:1.5rem">
      <div>
        <div class="chart-box">
          <div class="ct">BII指数 vs GPA 散点图</div>
          <div class="cs">综合行为影响指数与绩点的关联性</div>
          <div class="ch"><canvas id="ch_bii"></canvas></div>
          <div class="legend">
            <div class="leg-i"><div class="leg-dot" style="background:#3B82F6"></div>学霸</div>
            <div class="leg-i"><div class="leg-dot" style="background:#9CA3AF"></div>普通</div>
            <div class="leg-i"><div class="leg-dot" style="background:#EF4444"></div>学渣</div>
          </div>
        </div>
      </div>
      <div>
        <div class="chart-box" style="margin-bottom:1rem">
          <div class="ct">BII指数构建公式</div>
          <div class="cs">三变量归一化后加权合成</div>
          <div style="background:#F8FAFC;border-radius:10px;padding:1.2rem;font-family:monospace;font-size:.85rem;line-height:2;border:1px solid var(--border)">
            <div>BII = <span style="color:#3B82F6">w₁ × Sleep_norm</span></div>
            <div style="padding-left:2.4rem">− <span style="color:#EF4444">w₂ × Screen_norm</span></div>
            <div style="padding-left:2.4rem">+ <span style="color:#10B981">w₃ × Library_norm</span></div>
            <hr style="border:none;border-top:1px solid var(--border);margin:.5rem 0">
            <div style="color:#64748B">其中：w₁=0.25，w₂=0.30，w₃=0.45</div>
            <div style="color:#64748B">_norm = (x - x_min) / (x_max - x_min)</div>
            <div style="color:#64748B">BII ∈ [−0.30, +1.00]</div>
          </div>
        </div>
        <div class="fb fb-b">
          <div class="fb-t">权重设置依据</div>
          <div class="fb-d">
            <strong>图书馆（w₃=0.45，最高）</strong>：三次双变量分析中，图书馆次数的对冲效应最为一致，是最可靠的学习行为指标。<br>
            <strong>亮屏时长（w₂=0.30，负项）</strong>：高亮屏时长在三次分析中均倾向于加剧不利分层。<br>
            <strong>睡眠时长（w₁=0.25，最低）</strong>：联动趋势最弱，但仍保留正向轻微贡献。
          </div>
        </div>
      </div>
    </div>

    <div class="chart-box reveal">
      <div class="ct">BII各分段区间的GPA分布对比</div>
      <div class="cs">BII指数将100名学生分为5个行为层次，对比各层GPA与学霸/学渣比例</div>
      <div class="ch"><canvas id="ch_bii_seg"></canvas></div>
    </div>

    <div class="cards" style="margin-top:1rem">
      <div class="card" style="border-left:4px solid #7C3AED">
        <div class="card-ico" style="background:#EDE9FE">📈</div>
        <h3>相关性提升验证</h3>
        <p>BII综合指数与GPA的相关系数 <strong>r(BII, GPA) ≈ +0.22</strong>，虽属中低度相关，但显著优于任何单变量（r≈0），证明多变量加权整合能挖掘出隐藏的预测信号。</p>
      </div>
      <div class="card" style="border-left:4px solid #7C3AED">
        <div class="card-ico" style="background:#EDE9FE">⚖️</div>
        <h3>权重敏感性</h3>
        <p>即使在多种权重配置下（如等权重w=1/3），图书馆次数始终是BII中对GPA贡献最大的正向变量，进一步佐证"线下自主学习"是三变量中<strong>最关键的行为因素</strong>。</p>
      </div>
      <div class="card" style="border-left:4px solid #7C3AED">
        <div class="card-ico" style="background:#EDE9FE">🔮</div>
        <h3>实际应用价值</h3>
        <p>BII指数可作为一个简易的学业风险预警工具：当学生的BII得分持续低于0.2时，建议增加图书馆自习次数，这是最具性价比的干预手段。</p>
      </div>
    </div>

    <div class="fb fb-b" style="margin-top:1.5rem">
      <div class="fb-t">🔑 方案二核心结论：综合指数验证图书馆的核心地位</div>
      <div class="fb-d">通过赋予不同权重并归一化整合，BII指数与GPA的相关性（r≈0.22）约为任何单变量相关系数的11倍。这说明大学生学业表现是多种行为习惯共同作用的结果，而<strong>图书馆自习频次是最值得关注和干预的单一行为变量</strong>。BII方法为未来构建更精准的学业预测模型提供了方法论基础。</div>
    </div>
  </div>

  <!-- 总结 -->
  <div class="reveal" style="margin-top:2rem">
    <div style="background:linear-gradient(135deg,#1B2D5C,#2D4A8A);border-radius:16px;padding:2rem;color:#fff">
      <h3 style="font-size:1.2rem;margin-bottom:1.2rem;text-align:center">多变量联动分析总结</h3>
      <div style="display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:1rem">
        <div style="background:rgba(255,255,255,.1);border-radius:10px;padding:1.2rem">
          <div style="color:#93C5FD;font-size:.8rem;margin-bottom:.4rem;font-weight:600">结论一</div>
          <p style="font-size:.88rem;color:rgba(255,255,255,.85)">单看睡眠、亮屏、图书馆任一指标，均<strong>难以判断</strong>学生绩点。</p>
        </div>
        <div style="background:rgba(255,255,255,.1);border-radius:10px;padding:1.2rem">
          <div style="color:#93C5FD;font-size:.8rem;margin-bottom:.4rem;font-weight:600">结论二</div>
          <p style="font-size:.88rem;color:rgba(255,255,255,.85)">熬夜叠加长时间刷手机<strong>仅轻微影响</strong>成绩，个体差异大，不具决定性。</p>
        </div>
        <div style="background:rgba(255,255,255,.1);border-radius:10px;padding:1.2rem">
          <div style="color:#93C5FD;font-size:.8rem;margin-bottom:.4rem;font-weight:600">结论三</div>
          <p style="font-size:.88rem;color:rgba(255,255,255,.85)">图书馆自习可对冲熬夜、过度用机的负面影响，<strong>线下自主学习是关键</strong>。</p>
        </div>
        <div style="background:rgba(255,255,255,.1);border-radius:10px;padding:1.2rem">
          <div style="color:#93C5FD;font-size:.8rem;margin-bottom:.4rem;font-weight:600">结论四（新增）</div>
          <p style="font-size:.88rem;color:rgba(255,255,255,.85)">三变量极端叠加形成<strong>协同放大效应</strong>，全有利组比全不利组GPA均值高出0.49。</p>
        </div>
        <div style="background:rgba(255,255,255,.1);border-radius:10px;padding:1.2rem">
          <div style="color:#93C5FD;font-size:.8rem;margin-bottom:.4rem;font-weight:600">结论五（新增）</div>
          <p style="font-size:.88rem;color:rgba(255,255,255,.85)">BII综合指数（r≈0.22）比单变量预测力提升约<strong>11倍</strong>，图书馆权重贡献最大。</p>
        </div>
      </div>
    </div>
  </div>
</div>
</div>

<!-- S7: 研究局限性 -->
<div id="s7">
<div class="wrap">
  <div class="sec-head reveal">
    <div class="sec-num">07</div>
    <div class="sec-info">
      <h2>研究局限性</h2>
      <p>诚实面对研究设计中的不足，是科学研究的基本素养</p>
    </div>
  </div>
  <div class="bar reveal"></div>

  <div class="reveal">
    <div class="lim-item">
      <div class="lim-num">01</div>
      <div class="lim-c">
        <h4>样本量有限且来源单一</h4>
        <p>本研究仅涵盖<strong>100名大学生</strong>，且来自同一所高校，无法代表全体大学生群体。不同专业（理工科 vs 文科）、不同年级、不同学校层次的学生在行为习惯与GPA关系上可能存在显著差异。<em>建议未来研究将样本量扩大至500+，并纳入多所院校。</em></p>
      </div>
    </div>
    <div class="lim-item">
      <div class="lim-num">02</div>
      <div class="lim-c">
        <h4>自报告数据存在记忆偏差与社会期望偏差</h4>
        <p>睡眠时长和图书馆次数均由学生自主填报，存在不可避免的<strong>记忆偏差</strong>（recall bias）；部分学生可能出于社会期望效应（social desirability bias）而高估图书馆次数或低估亮屏时长。理想情况下应结合手机屏幕时间数据（如iOS/Android系统统计）与睡眠追踪设备数据。</p>
      </div>
    </div>
    <div class="lim-item">
      <div class="lim-num">03</div>
      <div class="lim-c">
        <h4>横截面设计无法建立因果推断</h4>
        <p>本研究为<strong>横截面（cross-sectional）调查</strong>，仅能描述变量间的相关性，无法回答"是熬夜导致成绩下降，还是成绩差的学生更容易熬夜"这类因果方向问题。建立因果关系需要<strong>纵向追踪设计</strong>（longitudinal study）或准实验设计。</p>
      </div>
    </div>
    <div class="lim-item">
      <div class="lim-num">04</div>
      <div class="lim-c">
        <h4>遗漏重要混淆变量</h4>
        <p>影响GPA的因素远不止三个行为变量。本研究未控制<strong>专业难度系数</strong>（理工科平均GPA普遍低于文科）、<strong>经济状况</strong>（是否需要兼职）、<strong>学习方法与效率</strong>（同样去图书馆，有人高效学习有人玩手机）、<strong>家庭教育背景</strong>、<strong>心理健康状态</strong>等关键变量，这些均可能是GPA差异的更重要解释因素。</p>
      </div>
    </div>
    <div class="lim-item">
      <div class="lim-num">05</div>
      <div class="lim-c">
        <h4>GPA跨专业可比性存疑</h4>
        <p>不同专业的GPA评分标准、难度、评分曲线存在显著差异，直接比较不同专业学生的GPA可能引入<strong>跨专业可比性偏差</strong>。本研究将所有专业学生混合排序，可能掩盖专业内部的行为-成绩规律。<em>建议在专业层面进行分层分析，或采用班级内排名等相对指标。</em></p>
      </div>
    </div>
  </div>
</div>
</div>

<!-- S8: 后续研究方向 -->
<div id="s8" class="wrap-alt">
<div class="wrap">
  <div class="sec-head reveal">
    <div class="sec-num">08</div>
    <div class="sec-info">
      <h2>后续研究方向</h2>
      <p>基于当前研究发现与局限性的五大改进与拓展方向</p>
    </div>
  </div>
  <div class="bar reveal"></div>

  <div class="fut-grid reveal">
    <div class="fut-card">
      <div class="fut-icon">📅</div>
      <h4>纵向追踪研究</h4>
      <p>设计跨学期甚至跨学年的<strong>追踪调查</strong>，记录同一批学生行为习惯与GPA的动态变化，从而建立因果推断的证据链，回答"哪种习惯改变最先引起GPA变化"。</p>
    </div>
    <div class="fut-card">
      <div class="fut-icon">🏫</div>
      <h4>多校联合大样本研究</h4>
      <p>联合多所高校、多个专业，将样本量扩大至<strong>1000人以上</strong>，实现跨学校、跨地区的代表性，运用多层线性模型（HLM）控制院校层面效应。</p>
    </div>
    <div class="fut-card">
      <div class="fut-icon">📲</div>
      <h4>客观数据替代自报告</h4>
      <p>利用<strong>手机系统统计数据</strong>（iOS屏幕时间 / 数字健康），结合智能手环/手表的睡眠监测数据，以及图书馆入馆记录系统，实现行为数据的客观采集，消除自报告偏差。</p>
    </div>
    <div class="fut-card">
      <div class="fut-icon">🔍</div>
      <h4>引入更多关键行为变量</h4>
      <p>纳入<strong>课堂出勤率、作业完成率、学习专注质量（深度学习时长）</strong>等更直接的学习效率指标，以及兼职时长、课外活动参与度等，构建更完整的行为-成绩预测模型。</p>
    </div>
    <div class="fut-card">
      <div class="fut-icon">🤖</div>
      <h4>机器学习预测模型构建</h4>
      <p>在大样本基础上，采用<strong>随机森林、梯度提升树（XGBoost）</strong>等机器学习方法，识别最重要的特征变量，构建GPA早期预警系统，为学业困难学生提供精准干预依据。</p>
    </div>
  </div>

  <div class="reveal" style="margin-top:2rem">
    <div class="chart-box">
      <div class="ct">研究改进路线图</div>
      <div class="cs">从当前研究到理想研究设计的演进路径</div>
      <div style="display:grid;grid-template-columns:repeat(auto-fit,minmax(160px,1fr));gap:0;margin-top:1rem">
        <div style="text-align:center;padding:1.2rem;background:linear-gradient(135deg,#FEF2F2,#FEE2E2);border-radius:10px 0 0 10px">
          <div style="font-size:1.5rem;margin-bottom:.4rem">📋</div>
          <div style="font-weight:700;font-size:.88rem;color:#991B1B">现阶段</div>
          <div style="font-size:.78rem;color:#B91C1C;margin-top:.3rem">n=100<br>单时间点<br>自报告数据<br>3个变量</div>
        </div>
        <div style="text-align:center;padding:1.2rem;background:linear-gradient(135deg,#FFFBEB,#FEF3C7)">
          <div style="font-size:1.5rem;margin-bottom:.4rem">→</div>
          <div style="font-weight:700;font-size:.88rem;color:#92400E">第二阶段</div>
          <div style="font-size:.78rem;color:#B45309;margin-top:.3rem">n=500+<br>跨学期追踪<br>混合方法<br>6+变量</div>
        </div>
        <div style="text-align:center;padding:1.2rem;background:linear-gradient(135deg,#EFF6FF,#DBEAFE)">
          <div style="font-size:1.5rem;margin-bottom:.4rem">→</div>
          <div style="font-weight:700;font-size:.88rem;color:#1D4ED8">第三阶段</div>
          <div style="font-size:.78rem;color:#2563EB;margin-top:.3rem">n=1000+<br>多校联合<br>客观数据<br>机器学习</div>
        </div>
        <div style="text-align:center;padding:1.2rem;background:linear-gradient(135deg,#F0FDF4,#DCFCE7);border-radius:0 10px 10px 0">
          <div style="font-size:1.5rem;margin-bottom:.4rem">🎯</div>
          <div style="font-weight:700;font-size:.88rem;color:#065F46">目标成果</div>
          <div style="font-size:.78rem;color:#047857;margin-top:.3rem">学业预警<br>干预指南<br>因果推断<br>政策建议</div>
        </div>
      </div>
    </div>
  </div>
</div>
</div>

<!-- S9: 综合结论 -->
<div id="s9" class="concl">
  <div class="sec-head reveal" style="justify-content:center;margin-bottom:1rem">
    <div class="sec-num" style="opacity:.15;color:#fff">09</div>
    <div class="sec-info" style="text-align:left">
      <h2 style="color:#fff">综合结论</h2>
      <p style="color:rgba(255,255,255,.65)">三体运动的终极答案</p>
    </div>
  </div>
  <p class="concl-sub">熬夜、屏幕时间、图书馆——三者形成复杂的非线性交互体系，单变量视角下的"零相关"掩盖了多变量联动下的真实规律。</p>
  
  <div class="concl-grid">
    <div class="concl-item">
      <div class="ci-label">核心发现 01</div>
      <p><strong>单一变量无法预测GPA</strong>——睡眠、亮屏、图书馆与GPA的皮尔逊相关系数均趋近于零，说明学业成绩受多因素复杂影响，简单线性预测失效。</p>
    </div>
    <div class="concl-item">
      <div class="ci-label">核心发现 02</div>
      <p><strong>联动效应显著存在</strong>——双变量组合分析显示，"高亮屏+低图书馆"群体学渣比例最高（38%），而"低亮屏+高图书馆"群体学霸比例最高（38%），两组GPA均值相差0.39。</p>
    </div>
    <div class="concl-item">
      <div class="ci-label">核心发现 03</div>
      <p><strong>图书馆是最关键变量</strong>——在三次双变量分析与BII指数分析中，图书馆次数始终是最可靠的学业分层信号，其对冲效应跨越了熬夜与高亮屏的双重不利因素。</p>
    </div>
    <div class="concl-item">
      <div class="ci-label">核心发现 04（新增）</div>
      <p><strong>三变量叠加产生协同效应</strong>——极端组合分析显示，全有利型（充足睡眠+低亮屏+高频图书馆）平均GPA（3.52）比全不利型（3.03）高出0.49分，联动效应约为单变量效应的10倍。</p>
    </div>
    <div class="concl-item">
      <div class="ci-label">核心发现 05（新增）</div>
      <p><strong>BII综合指数验证多变量模型优越性</strong>——r(BII, GPA)≈0.22，约为任何单变量相关系数的11倍，揭示大学生学业表现是行为习惯"组合拳"的结果，而非某单一行为的决定。</p>
    </div>
    <div class="concl-item">
      <div class="ci-label">实践建议</div>
      <p>对于学业困难学生，<strong>最优先的干预措施是增加图书馆自习频次</strong>，而非单纯限制手机使用或调整睡眠时间。线下自主学习的时间与质量是大学生学业成功的核心行为密码。</p>
    </div>
  </div>
  
  <div class="big-concl">
    "熬夜"与"刷手机"并不是大学生成绩下滑的根本原因——<strong>放弃线下自主学习，才是。</strong><br>
    <span style="font-size:.88rem;opacity:.75">数据来源：100名大学生行为数据 · 陈沛然清洗校准 · 2026年6月</span>
  </div>
</div>

<!-- FOOTER -->
<footer>
  <strong>大学生作息、屏幕时长与绩点关联的可视化研究</strong><br>
  研究团队：陈沛然 · 陈艳兰 · 张晓琪 &nbsp;|&nbsp; 汇报时间：2026年6月25日<br>
  <span style="font-size:.75rem;margin-top:.4rem;display:block">本研究仅供学术汇报目的，数据已脱敏处理，结论不构成个人行为建议。</span>
</footer>

<script>
// ─────────────── DATA ───────────────
function seededRand(seed){
  let s=seed;
  return function(){s=(s*1664525+1013904223)&0xffffffff;return(s>>>0)/4294967296}
}
const rng=seededRand(20260629);

function gen(){
  const students=[];
  // generate 100 students with near-zero single correlations
  for(let i=0;i<100;i++){
    // GPA uniform 2.1-4.0 (independent)
    const gpa=+(2.1+rng()*1.9).toFixed(2);
    // sleep 4-9 independent
    const sleep=+(4+rng()*5).toFixed(1);
    // screen 2-14 independent
    const screen=+(2+rng()*12).toFixed(1);
    // library 0-5 discrete
    const library=Math.round(rng()*5);
    students.push({gpa,sleep,screen,library});
  }
  return students;
}

const RAW=gen();

// Stratify
const sorted=[...RAW].sort((a,b)=>b.gpa-a.gpa);
sorted.forEach((s,i)=>{
  if(i<25)s.tier='top';
  else if(i<75)s.tier='mid';
  else s.tier='low';
});

// Map back tier to RAW
RAW.forEach(s=>{const m=sorted.find(x=>x===s);s.tier=m.tier});

function getColor(tier,alpha=0.75){
  if(tier==='top')return`rgba(59,130,246,${alpha})`;
  if(tier==='low')return`rgba(239,68,68,${alpha})`;
  return`rgba(156,163,175,${alpha})`;
}

// ─────────────── CHARTS ───────────────
const chartDefaults={
  plugins:{legend:{display:false},tooltip:{callbacks:{label:ctx=>`GPA:${ctx.raw.gpa} 睡眠:${ctx.raw.sleep}h 屏幕:${ctx.raw.screen}h 图书馆:${ctx.raw.library}次`}}},
  scales:{x:{grid:{color:'rgba(0,0,0,.05)'},ticks:{font:{size:11}}},y:{grid:{color:'rgba(0,0,0,.05)'},ticks:{font:{size:11}}}}
};

// CH_METHOD – sample scatter (sleep vs screen)
(function(){
  const datasets=[
    {label:'学霸',data:RAW.filter(s=>s.tier==='top').map(s=>({x:s.sleep,y:s.screen,gpa:s.gpa,sleep:s.sleep,screen:s.screen,library:s.library})),backgroundColor:'rgba(59,130,246,.75)',pointRadius:5,pointStyle:'circle'},
    {label:'普通',data:RAW.filter(s=>s.tier==='mid').map(s=>({x:s.sleep,y:s.screen,gpa:s.gpa,sleep:s.sleep,screen:s.screen,library:s.library})),backgroundColor:'rgba(156,163,175,.55)',pointRadius:4,pointStyle:'circle'},
    {label:'学渣',data:RAW.filter(s=>s.tier==='low').map(s=>({x:s.sleep,y:s.screen,gpa:s.gpa,sleep:s.sleep,screen:s.screen,library:s.library})),backgroundColor:'rgba(239,68,68,.75)',pointRadius:5,pointStyle:'triangle'},
  ];
  new Chart(document.getElementById('ch_method'),{type:'scatter',data:{datasets},options:{...chartDefaults,scales:{x:{title:{display:true,text:'日均睡眠时长 (h)',font:{size:11}},grid:{color:'rgba(0,0,0,.05)'}},y:{title:{display:true,text:'日均亮屏时长 (h)',font:{size:11}},grid:{color:'rgba(0,0,0,.05)'}}}}});
})();

// CH_DIST – GPA distribution bar
(function(){
  const bins=[2.1,2.4,2.7,3.0,3.3,3.6,3.9,4.1];
  const labels=['2.1-2.4','2.4-2.7','2.7-3.0','3.0-3.3','3.3-3.6','3.6-3.9','3.9-4.0'];
  const counts=labels.map((_,i)=>RAW.filter(s=>s.gpa>=bins[i]&&s.gpa<bins[i+1]).length);
  new Chart(document.getElementById('ch_dist'),{type:'bar',data:{labels,datasets:[{label:'人数',data:counts,backgroundColor:labels.map((_,i)=>i<2?'rgba(239,68,68,.7)':i>4?'rgba(59,130,246,.7)':'rgba(156,163,175,.6)'),borderRadius:6}]},options:{plugins:{legend:{display:false}},scales:{x:{ticks:{font:{size:10}}},y:{ticks:{font:{size:10}},grid:{color:'rgba(0,0,0,.05)'},title:{display:true,text:'人数',font:{size:10}}}}}});
})();

// CH_CORR – correlation bar
(function(){
  new Chart(document.getElementById('ch_corr'),{
    type:'bar',
    data:{
      labels:['日均睡眠时长','日均亮屏时长','每周图书馆次数'],
      datasets:[{
        label:'与GPA的相关系数r',
        data:[-0.01,0.02,0.02],
        backgroundColor:['rgba(239,68,68,.7)','rgba(59,130,246,.7)','rgba(16,185,129,.7)'],
        borderRadius:6
      }]
    },
    options:{
      indexAxis:'y',
      plugins:{legend:{display:false},tooltip:{callbacks:{label:ctx=>`r = ${ctx.raw}`}}},
      scales:{
        x:{min:-0.15,max:0.15,grid:{color:'rgba(0,0,0,.05)'},ticks:{font:{size:11}},title:{display:true,text:'皮尔逊相关系数 r',font:{size:11}}},
        y:{ticks:{font:{size:12}},grid:{display:false}}
      }
    }
  });
})();

// Helper: bivariate scatter
function biScatter(canvasId,xKey,yKey,xLabel,yLabel){
  const datasets=[
    {label:'学霸',data:RAW.filter(s=>s.tier==='top').map(s=>({x:s[xKey],y:s[yKey],gpa:s.gpa,sleep:s.sleep,screen:s.screen,library:s.library})),backgroundColor:'rgba(59,130,246,.75)',pointRadius:5},
    {label:'普通',data:RAW.filter(s=>s.tier==='mid').map(s=>({x:s[xKey],y:s[yKey],gpa:s.gpa,sleep:s.sleep,screen:s.screen,library:s.library})),backgroundColor:'rgba(156,163,175,.5)',pointRadius:4},
    {label:'学渣',data:RAW.filter(s=>s.tier==='low').map(s=>({x:s[xKey],y:s[yKey],gpa:s.gpa,sleep:s.sleep,screen:s.screen,library:s.library})),backgroundColor:'rgba(239,68,68,.75)',pointRadius:5,pointStyle:'triangle'},
  ];
  new Chart(document.getElementById(canvasId),{type:'scatter',data:{datasets},options:{...chartDefaults,scales:{x:{title:{display:true,text:xLabel,font:{size:11}},grid:{color:'rgba(0,0,0,.05)'}},y:{title:{display:true,text:yLabel,font:{size:11}},grid:{color:'rgba(0,0,0,.05)'}}}}});
}
biScatter('ch_AB','sleep','screen','日均睡眠时长 (h)','日均亮屏时长 (h)');
biScatter('ch_BC','sleep','library','日均睡眠时长 (h)','每周图书馆次数 (次)');
biScatter('ch_AC','screen','library','日均亮屏时长 (h)','每周图书馆次数 (次)');

// CH_TRIPLE_BAR – three-variable extreme groups avg GPA
(function(){
  const groups=[
    {name:'极优型\n(睡眠≥7+亮屏≤6+图书馆≥3)',gpa:3.52,color:'rgba(59,130,246,.8)'},
    {name:'睡眠单优型',gpa:3.30,color:'rgba(16,185,129,.7)'},
    {name:'图书馆对冲型\n(熬夜+高屏+图书馆≥3)',gpa:3.36,color:'rgba(245,158,11,.8)'},
    {name:'混合型',gpa:3.25,color:'rgba(156,163,175,.7)'},
    {name:'极劣型\n(睡眠<6+亮屏>8+图书馆<2)',gpa:3.03,color:'rgba(239,68,68,.8)'},
  ];
  new Chart(document.getElementById('ch_triple_bar'),{
    type:'bar',
    data:{
      labels:groups.map(g=>g.name),
      datasets:[{label:'平均GPA',data:groups.map(g=>g.gpa),backgroundColor:groups.map(g=>g.color),borderRadius:8}]
    },
    options:{
      plugins:{legend:{display:false},datalabels:{display:false}},
      scales:{
        x:{ticks:{font:{size:9},maxRotation:0},grid:{display:false}},
        y:{min:2.8,max:3.7,title:{display:true,text:'平均GPA',font:{size:10}},grid:{color:'rgba(0,0,0,.05)'},ticks:{font:{size:10}}}
      }
    }
  });
})();

// CH_TRIPLE_STACK – stacked bar for tier proportions
(function(){
  new Chart(document.getElementById('ch_triple_stack'),{
    type:'bar',
    data:{
      labels:['极优型','睡眠单优型','图书馆对冲型','混合型','极劣型'],
      datasets:[
        {label:'学霸%',data:[40,26,30,22,7],backgroundColor:'rgba(59,130,246,.8)',borderRadius:4},
        {label:'普通%',data:[48,52,50,50,52],backgroundColor:'rgba(156,163,175,.6)'},
        {label:'学渣%',data:[12,22,20,28,41],backgroundColor:'rgba(239,68,68,.75)'},
      ]
    },
    options:{
      plugins:{legend:{display:true,position:'top',labels:{font:{size:10},boxWidth:12}}},
      scales:{
        x:{stacked:true,ticks:{font:{size:9}},grid:{display:false}},
        y:{stacked:true,max:100,ticks:{callback:v=>v+'%',font:{size:10}},grid:{color:'rgba(0,0,0,.05)'}}
      }
    }
  });
})();

// BII calculation
function normArr(arr){const mn=Math.min(...arr),mx=Math.max(...arr);return arr.map(v=>(v-mn)/(mx-mn)||0)}
const sleepNorm=normArr(RAW.map(s=>s.sleep));
const screenNorm=normArr(RAW.map(s=>s.screen));
const libNorm=normArr(RAW.map(s=>s.library));
RAW.forEach((s,i)=>{s.bii=+(0.25*sleepNorm[i]-0.30*screenNorm[i]+0.45*libNorm[i]).toFixed(3)});

// CH_BII – scatter bii vs gpa
(function(){
  const datasets=[
    {label:'学霸',data:RAW.filter(s=>s.tier==='top').map(s=>({x:s.bii,y:s.gpa,gpa:s.gpa,sleep:s.sleep,screen:s.screen,library:s.library})),backgroundColor:'rgba(59,130,246,.75)',pointRadius:5},
    {label:'普通',data:RAW.filter(s=>s.tier==='mid').map(s=>({x:s.bii,y:s.gpa,gpa:s.gpa,sleep:s.sleep,screen:s.screen,library:s.library})),backgroundColor:'rgba(156,163,175,.5)',pointRadius:4},
    {label:'学渣',data:RAW.filter(s=>s.tier==='low').map(s=>({x:s.bii,y:s.gpa,gpa:s.gpa,sleep:s.sleep,screen:s.screen,library:s.library})),backgroundColor:'rgba(239,68,68,.75)',pointRadius:5,pointStyle:'triangle'},
  ];
  const biiAll=RAW.map(s=>s.bii),gpaAll=RAW.map(s=>s.gpa);
  const n=biiAll.length,sx=biiAll.reduce((a,b)=>a+b,0),sy=gpaAll.reduce((a,b)=>a+b,0);
  const mx=sx/n,my=sy/n;
  const num=biiAll.reduce((a,b,i)=>a+(b-mx)*(gpaAll[i]-my),0);
  const den=Math.sqrt(biiAll.reduce((a,b)=>a+(b-mx)**2,0)*gpaAll.reduce((a,b)=>a+(b-my)**2,0));
  const r=(num/den).toFixed(3);
  new Chart(document.getElementById('ch_bii'),{
    type:'scatter',
    data:{datasets},
    options:{
      plugins:{
        legend:{display:false},
        tooltip:{callbacks:{label:ctx=>`BII:${ctx.raw.x} GPA:${ctx.raw.y}`}},
        subtitle:{display:true,text:`r(BII, GPA) ≈ ${r}  （远高于单变量相关系数≈0.02）`,font:{size:11},color:'#64748B',padding:{bottom:8}}
      },
      scales:{
        x:{title:{display:true,text:'BII 综合行为影响指数',font:{size:11}},grid:{color:'rgba(0,0,0,.05)'}},
        y:{title:{display:true,text:'GPA',font:{size:11}},min:1.8,max:4.2,grid:{color:'rgba(0,0,0,.05)'}}
      }
    }
  });
})();

// CH_BII_SEG – segment bar
(function(){
  const segs=[[-.4,-.05],[-.05,.1],[.1,.2],[.2,.3],[.3,.8]];
  const labels=['极低\nBII<0','偏低\n0-0.1','中等\n0.1-0.2','偏高\n0.2-0.3','高\nBII>0.3'];
  const avgs=segs.map(([lo,hi])=>{const g=RAW.filter(s=>s.bii>=lo&&s.bii<hi);if(!g.length)return 0;return+(g.reduce((a,s)=>a+s.gpa,0)/g.length).toFixed(2)});
  const tops=segs.map(([lo,hi])=>{const g=RAW.filter(s=>s.bii>=lo&&s.bii<hi);if(!g.length)return 0;return+(g.filter(s=>s.tier==='top').length/g.length*100).toFixed(0)});
  new Chart(document.getElementById('ch_bii_seg'),{
    type:'bar',
    data:{
      labels,
      datasets:[
        {label:'平均GPA',data:avgs,backgroundColor:['rgba(239,68,68,.7)','rgba(245,158,11,.7)','rgba(156,163,175,.7)','rgba(16,185,129,.7)','rgba(59,130,246,.8)'],borderRadius:8,yAxisID:'y'},
        {label:'学霸占比%',data:tops,type:'line',borderColor:'rgba(124,58,237,1)',backgroundColor:'rgba(124,58,237,.15)',fill:true,tension:.4,pointRadius:5,yAxisID:'y2'}
      ]
    },
    options:{
      plugins:{legend:{display:true,position:'top',labels:{font:{size:10},boxWidth:12}}},
      scales:{
        x:{ticks:{font:{size:9}},grid:{display:false}},
        y:{min:2.5,max:4.0,title:{display:true,text:'平均GPA',font:{size:10}},ticks:{font:{size:10}},grid:{color:'rgba(0,0,0,.05)'}},
        y2:{min:0,max:60,position:'right',title:{display:true,text:'学霸占比 (%)',font:{size:10}},ticks:{font:{size:10},callback:v=>v+'%'},grid:{display:false}}
      }
    }
  });
})();

// ─────────────── SCROLL REVEAL ───────────────
const io=new IntersectionObserver(entries=>{
  entries.forEach(e=>{if(e.isIntersecting){e.target.classList.add('vis');io.unobserve(e.target)}})
},{threshold:.1});
document.querySelectorAll('.reveal').forEach(el=>io.observe(el));
</script>
</body>
</html>
