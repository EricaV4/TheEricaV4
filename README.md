<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FoxyMomos</title>
    <link href="https://cdn.bootcdn.net/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
	
    <style>
	
	
	
        :root {
            --primary-color: #2c7be5;
            --sidebar-width: 240px;
            --card-width: 330px;
            --card-height: 160px;
            --banner-height: 90px;  /* 增大横幅高度 */
        }
		
		body {
            font-family: 'Segoe UI', system-ui, sans-serif;
            background: #dbdaec; /* 背景颜色 */
            display: flex;
            min-height: 100vh;
        }
	
		.card-container {
            display: grid;
            /* 设置行间距为3rem，列间距为2rem */
            gap: 3rem 2rem;  /* 第一个值控制行间距，第二个控制列间距 */
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            padding: 1rem 0;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        /* 侧边栏样式 */
        .sidebar {
            width: var(--sidebar-width);
            background: white;
            padding: 1.5rem;
            position: fixed;
            height: 100vh;
            box-shadow: 2px 0 12px rgba(0,0,0,0.05);
            overflow-y: auto;
        }

        .nav-title {
            color: var(--primary-color);
            font-size: 1.2rem;
            margin: 1rem 0;
            padding-left: 0.5rem;
        }

        .nav-menu {
            list-style: none;
        }

        .nav-item {
            margin: 0.6rem 0;
        }

        .nav-link {
            display: flex;
            align-items: center;
            padding: 0.8rem 1rem;
            border-radius: 8px;
            color: #4a5568;
            text-decoration: none;
            transition: all 0.2s;
        }

        .nav-link:hover {
            background: #f1f5f9;
            color: var(--primary-color);
        }

        .nav-icon {
            width: 24px;
            margin-right: 1rem;
            text-align: center;
        }

        /* 主内容区 */
        .main-content {
            flex: 1;
            margin-left: var(--sidebar-width);
            padding: 2rem;
            max-width: 1400px;
        }
		
		.main-banner {
            height: var(--banner-height);
            background: linear-gradient(45deg, #2c7be5, #6a11cb);
            margin-bottom: 2rem;
            border-radius: 12px;
            position: relative;
            overflow: hidden;
            opacity: 0;
            transform: translateY(-50px);
            animation: bannerEntrance 1s cubic-bezier(0.4, 0, 0.2, 1) forwards;
        }

        @keyframes bannerEntrance {
            0% {
                opacity: 0;
                transform: translateY(-50px);
            }
            100% {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .banner-text {
            color: white;
            font-size: 2.5rem;
            text-align: center;
            position: relative;
            z-index: 1;
            opacity: 0;
            animation: textAppear 1s 0.5s forwards;
        }
		
		.banner-text {
            color: white;
            font-size: 2.2rem;  /* 横幅字体大小 */
            text-align: center;
            position: relative;
            z-index: 1;
            opacity: 0;
            animation: textAppear 1s 0.5s forwards;
            display: flex;
            align-items: center;
            justify-content: center;
            height: 100%;
            margin: 0;
            text-shadow: 3px 3px 6px rgba(0,0,0,0.5);
            letter-spacing: 2px;  /* 增加字间距 */
        }
		
        @keyframes textAppear {
            0% {
                opacity: 0;
                transform: scale(0.9);
            }
            100% {
                opacity: 1;
                transform: scale(1);
            }
        }


        .banner-particle {
            position: absolute;
            background: rgba(255,255,255,0.2);
            border-radius: 50%;
            animation: particleMove 4s infinite;
        }

        @keyframes particleMove {
            0% {
                transform: translateY(0) translateX(0);
                opacity: 0;
            }
            50% {
                opacity: 0.3;
            }
            100% {
                transform: translateY(-100px) translateX(50px);
                opacity: 0;
            }
        }

        /* 分类标题 */
        .section-title {
            color: var(--primary-color);
            font-size: 1.4rem;
            margin: 2rem 0 1.5rem;
            padding-left: 0.8rem;
            border-left: 4px solid var(--primary-color);
        }

        /* 修复卡片布局 */
        .card-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 1.5rem;
            justify-content: center;
        }

        /* 卡片链接样式 */
        .card-link {
            display: block;
            text-decoration: none;
            color: inherit;
            transition: transform 0.2s;
        }

        .card-link:hover .fixed-card {
            transform: translateY(-5px);
            box-shadow: 0 8px 20px rgba(0,0,0,0.12);
        }

        /* 卡片样式 */
        .fixed-card {
            width: 100%;
            height: var(--card-height);
            background: white;
            border-radius: 12px;
            padding: 1.5rem;
            box-shadow: 0 2px 6px rgba(0,0,0,0.05);
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            color: #333;
        }

        .card-header {
            display: flex;
            align-items: center;
            margin-bottom: 1rem;
        }

        .card-icon {
            width: 40px;
            height: 40px;
            background: var(--primary-color);
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            margin-right: 1rem;
        }

        .card-icon.img-box {
            background: none;
            border: 1px solid #eee;
            padding: 2px;
        }

        .card-icon img {
            width: 100%;
            height: 100%;
            object-fit: contain;
        }

        .card-content {
            flex: 1;
            overflow-y: auto;
            padding-right: 8px;
        }

        .card-content p {
            color: #666;
            margin: 0;
            line-height: 1.6;
        }

        /* 响应式设计 */
        @media (max-width: 768px) {
            .sidebar {
                display: none;
            }
            .main-content {
                margin-left: 0;
                padding: 1rem;
            }
            .fixed-card {
                height: auto;
                min-height: 160px;
            }
            .section-title {
                font-size: 1.2rem;
                margin: 1.5rem 0 1rem;
            }
            .card-container {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>

<!--看什么呢 哼~-->
<body>
    <!-- 左侧导航栏 -->
    <nav class="sidebar">
        <h2 class="nav-title"><i class="nav-icon fas fa-compass"></i>By EricaV4</h2>
        <ul class="nav-menu">
		
            <li class="nav-item">
                <a href="#Free-Client-new" class="nav-link">
                    高版本客户端
                </a>
            </li>
			
            <li class="nav-item">
                <a href="#Free-Client-old" class="nav-link">
                    低版本客户端
                </a>
            </li>
			
			<li class="nav-item">
                <a href="#Paid-Client" class="nav-link">
                    付费高版本客户端
                </a>
            </li>
			
			<li class="nav-item">
                <a href="#Free-inject" class="nav-link">
                    免费热注入
                </a>
            </li>
			
			<li class="nav-item">
                <a href="#Paid-inject" class="nav-link">
                    付费热注入
                </a>
            </li>
			
			<li class="nav-item">
                <a href="#PVP-Client" class="nav-link">
                    合法客户端
                </a>
            </li>
			
        </ul>
    </nav>

    <!-- 主内容区 -->
    <main class="main-content">
	 <div class="main-banner">
<script>
document.addEventListener('DOMContentLoaded', () => {
    const banner = document.querySelector('.main-banner');
    
    for (let i = 0; i < 100; i++) {
        const particle = document.createElement('div');
        particle.className = 'banner-particle';
        
        // 随机属性
        const size = Math.floor(Math.random() * 8 + 4); // 4-12px
        const left = Math.random() * 90 + 10; // 5%-95%
        const top = Math.random() * 90 + 20; // 10%-90%
        
        particle.style.cssText = `
            width: ${size}px;
            height: ${size}px;
            left: ${left}%;
            top: ${top}%;
        `;
        
        banner.insertBefore(particle, banner.firstChild);
    }
});

 // 平滑滚动函数
        function smoothScroll(targetId) {
            const target = document.querySelector(targetId);
            const sidebarWidth = parseInt(getComputedStyle(document.documentElement)
                .getPropertyValue('--sidebar-width'));
            const offset = 20; // 额外偏移量
            
            if (target) {
                const targetPosition = target.offsetTop - sidebarWidth - offset;
                const startPosition = window.pageYOffset;
                const distance = targetPosition - startPosition;
                const duration = 500; // 动画持续时间
                let startTime = null;

                function animation(currentTime) {
                    if (!startTime) startTime = currentTime;
                    const timeElapsed = currentTime - startTime;
                    const progress = Math.min(timeElapsed / duration, 1);
                    
                    window.scrollTo(0, startPosition + distance * easeInOutQuad(progress));
                    
                    if (timeElapsed < duration) {
                        requestAnimationFrame(animation);
                    }
                }

                // 缓动函数
                function easeInOutQuad(t) {
                    return t < 0.5 ? 2 * t * t : -1 + (4 - 2 * t) * t;
                }

                requestAnimationFrame(animation);
            }
        }

        // 绑定导航点击事件
        document.querySelectorAll('.nav-link').forEach(link => {
            link.addEventListener('click', function(e) {
                e.preventDefault();
                const targetId = this.getAttribute('href');
                history.replaceState(null, null, targetId); // 更新URL hash
                smoothScroll(targetId);
            });
        });

        // 激活状态追踪
        window.addEventListener('scroll', () => {
            const sections = document.querySelectorAll('section');
            const scrollPosition = window.pageYOffset + document.querySelector('.sidebar').offsetHeight + 50;
            
            sections.forEach(section => {
                const sectionTop = section.offsetTop;
                const sectionHeight = section.offsetHeight;
                
                if (scrollPosition >= sectionTop && scrollPosition < sectionTop + sectionHeight) {
                    const id = section.getAttribute('id');
                    document.querySelector(`.nav-link[href="#${id}"]`).classList.add('active');
                } else {
                    document.querySelector(`.nav-link[href="#${id}"]`).classList.remove('active');
                }
            });
        });

</script>
            <h1 class="banner-text">Welcome to FoxyMoMos</h1>
        </div>
        <!-- 免费客户端 -->
        <section id="Free-Client-new">
            <h2 class="section-title">免费,开源高版本客户端</h2>
            <div class="card-container">
                <!-- LiquidBounce -->
                <a href="https://cn.liquidbounce.net/" class="card-link" target="_blank" rel="noopener noreferrer">
                    <div class="fixed-card">
                        <div class="card-header">
                            <div class="card-icon img-box">
                                <img src="icon/lb.png">
                            </div>
                            <h3>LiquidBounce</h3>
                        </div>
                        <div class="card-content">
                            <p>全方面发展客户端<br />简洁的客户端 稳定更新 德国</p>
                        </div>
                    </div>
                </a>

                <!-- Meteor -->
                <a href="https://meteorclient.com/" class="card-link" target="_blank" rel="noopener noreferrer">
                    <div class="fixed-card"> 
                        <div class="card-header">
                            <div class="card-icon img-box">
                                <img src="icon/Meteor.png">
                            </div>
                            <h3>Meteor</h3>
                        </div>
                        <div class="card-content">
                            <p>水晶PVP客户端<br />自定义化HUD 美国</p>
                        </div>
                    </div>
                </a>

                <!-- ThunderHack -->
                <a href="https://github.com/Pan4ur/ThunderHack-Recode/releases/tag/latest" class="card-link" target="_blank" rel="noopener noreferrer">
                    <div class="fixed-card">
                        <div class="card-header">
                            <div class="card-icon img-box">
                                <img src="icon/Thunder.png">
                            </div>
                            <h3>ThunderHack</h3>
                        </div>
                        <div class="card-content">
                            <p>多模块水晶PVP客户端<br />为水晶与剑HVH开发 俄罗斯 <停更></p>
                        </div>
                    </div>
                </a>
            
			
			<!-- Wurst -->
                <a href="https://www.wurstclient.net/" class="card-link" target="_blank" rel="noopener noreferrer">
                    <div class="fixed-card">
                        <div class="card-header">
                            <div class="card-icon img-box">
                                <img src="icon/Wurst.png">
                            </div>
                            <h3>Wurst</h3>
                        </div>
                        <div class="card-content">
                            <p>多模块客户端<br />对无反作弊服务器的强力绕过 国外</p>
                        </div>
                    </div>
                </a>
            </div>
			
			<div class="card-container">
			
			<a href="https://github.com/ExceptionTeam6969/Sakura" class="card-link" target="_blank" rel="noopener noreferrer">
                    <div class="fixed-card">
                        <div class="card-header">
                            <div class="card-icon img-box">
                                <img src="icon/Sakura.png">
                            </div>
                            <h3>Sakura</h3>
                        </div>
                        <div class="card-content">
                            <p>水晶PVP客户端<br />搭配其他客户端使用 兼容性良一般 冷门 国外</p>
                        </div>
                    </div>
                </a>
				
				<a href="https://www.aobaclient.com/" class="card-link" target="_blank" rel="noopener noreferrer">
                    <div class="fixed-card">
                        <div class="card-header">
                            <div class="card-icon img-box">
                                <img src="icon/AoBa.png">
                            </div>
                            <h3>Aoba</h3>
                        </div>
                        <div class="card-content">
                            <p>轻量客户端<br />有密码破解器的凑数客户端 冷门 国外</p>
                        </div>
                    </div>
                </a>
				
				<a href="https://aristois.net/" class="card-link" target="_blank" rel="noopener noreferrer">
                    <div class="fixed-card">
                        <div class="card-header">
                            <div class="card-icon img-box">
                                <img src="icon/Aristois.png">
                            </div>
                            <h3>Aristois</h3>
                        </div>
                        <div class="card-content">
                            <p>生存客户端<br />强力的生存客户端 安装复杂 冷门 国外</p>
                        </div>
                    </div>
                </a>
				
			</div>
			
			<div class="card-container">
			
			<a href="https://github.com/CrytoPal/Continued-Salhack" class="card-link" target="_blank" rel="noopener noreferrer">
                    <div class="fixed-card">
                        <div class="card-header">
                            <div class="card-icon img-box">
                                <img src="icon/E4.png">
                            </div>
                            <h3>Salhack</h3>
                        </div>
                        <div class="card-content">
                            <p>1.20.4水晶PVP客户端<br />不知名客户端 多模块 冷门 国外</p>
                        </div>
                    </div>
                </a>
				
				<a href="https://1minecraft.net/coffee-client/" class="card-link" target="_blank" rel="noopener noreferrer">
                    <div class="fixed-card">
                        <div class="card-header">
                            <div class="card-icon img-box">
                                <img src="icon/coffee.png">
                            </div>
                            <h3>coffee</h3>
                        </div>
                        <div class="card-content">
                            <p>1.19.2-3客户端<br />不知名客户端 多模块 冷门 国外</p>
                        </div>
                    </div>
                </a>
				
				<a href="https://bleachhack.org/" class="card-link" target="_blank" rel="noopener noreferrer">
                    <div class="fixed-card">
                        <div class="card-header">
                            <div class="card-icon img-box">
                                <img src="icon/Bleach.png">
                            </div>
                            <h3>bleach</h3>
                        </div>
                        <div class="card-content">
                            <p>1.20.4客户端<br />轻量的不知名客户端 多模块 国外</p>
                        </div>
                    </div>
                </a>
			
			</div>
			
        </section>
		<!--                                免费低版本客户端                                 -->
				<section id="Free-Client-old">
            <h2 class="section-title">免费,开源1.8.9客户端</h2>
            <div class="card-container">
                <!-- LiquidBounce -->
                <a href="https://cn.liquidbounce.net/" class="card-link" target="_blank" rel="noopener noreferrer">
                    <div class="fixed-card">
                        <div class="card-header">
                            <div class="card-icon img-box">
                                <img src="icon/lb.png">
                            </div>
                            <h3>LiquidBounce legacy</h3>
                        </div>
                        <div class="card-content">
                            <p>遗产<br />高度自定义HUD 稳定更新 德国 <停更></p>
                        </div>
                    </div>
                </a>
				
				<a href="https://github.com/xia-mc/Raven-XD" class="card-link" target="_blank" rel="noopener noreferrer">
                    <div class="fixed-card">
                        <div class="card-header">
                            <div class="card-icon img-box">
                                <img src="icon/RavenXD.png">
                            </div>
                            <h3>Raven XD</h3>
                        </div>
                        <div class="card-content">
                            <p>xia_mc的客户端<br />基于Raven BS 集百家之长 国内 <停更></p>
                        </div>
                    </div>
                </a>
				
				<a href="https://github.com/xia-mc/Raven-XD" class="card-link" target="_blank" rel="noopener noreferrer">
                    <div class="fixed-card">
                        <div class="card-header">
                            <div class="card-icon img-box">
                                <img src="icon/MoonLight.png">
                            </div>
                            <h3>MoonLight</h3>
                        </div>
                        <div class="card-content">
                            <p>月光 适配性差<br />最好的视觉打滑端 国内 <不稳定></p>
                        </div>
                    </div>
                </a>
				
				
				
				</div>
				<div class="card-container">
				<a href="https://github.com/xia-mc/Raven-XD" class="card-link" target="_blank" rel="noopener noreferrer">
                    <div class="fixed-card">
                        <div class="card-header">
                            <div class="card-icon img-box">
                                <img src="icon/FDP.png">
                            </div>
                            <h3>FDP</h3>
                        </div>
                        <div class="card-content">
                            <p>基于LB 低版本客户端<br />这个打滑端的作用太少了 国外</p>
                        </div>
                    </div>
                </a>
				</div>
        </section>

			<!-- 1.12.2 -->
            <h2 class="section-title">免费,开源1.12.2客户端</h2>
            <div class="card-container">
                <a href="https://github.com/EricaV4/ThunderHackPlus/releases/tag/A" class="card-link" target="_blank" rel="noopener noreferrer">
                    <div class="fixed-card">
                        <div class="card-header">
                            <div class="card-icon img-box">
                                <img src="icon/Thunder.png">
                            </div>
                            <h3>ThunderHack Plus</h3>
                        </div>
                        <div class="card-content">
                            <p>低版本水晶PVP客户端<br />美丽的HUD 多模块 俄罗斯 <消失></p>
                        </div>
                    </div>
                </a>
				
				<a href="https://github.com/3arthqu4ke/3arthh4ck" class="card-link" target="_blank" rel="noopener noreferrer">
                    <div class="fixed-card">
                        <div class="card-header">
                            <div class="card-icon img-box">
                                <img src="icon/E4.png">
                            </div>
                            <h3>3arthh4ck</h3>
                        </div>
                        <div class="card-content">
                            <p>以前最的强势客户端<br />有着不俗的水晶PVP能力 国外 <停更></p>
                        </div>
                    </div>
                </a>
				
				<a href="https://github.com/hf2kxn/Hyperlethal-Client" class="card-link" target="_blank" rel="noopener noreferrer">
                    <div class="fixed-card">
                        <div class="card-header">
                            <div class="card-icon img-box">
                                <img src="icon/HyperLethal.png">
                            </div>
                            <h3>HyperLethal</h3>
                        </div>
                        <div class="card-content">
                            <p>21年强势客户端<br />优秀的客户端 国外 <停更></p>
                        </div>
                    </div>
                </a>
				
				
				
				</div>
				<div class="card-container">
				<a href="https://github.com/h0rb/Phobos-1.9.0_Clean-and-Compatible" class="card-link" target="_blank" rel="noopener noreferrer">
                    <div class="fixed-card">
                        <div class="card-header">
                            <div class="card-icon img-box">
                                <img src="icon/E4.png">
                            </div>
                            <h3>Phobos</h3>
                        </div>
                        <div class="card-content">
                            <p>陌生的客户端<br />在角落的客户端 <停更></p>
                        </div>
                    </div>
                </a>
				
				<a href="https://github.com/CreepyOrb924/creepy-salhack" class="card-link" target="_blank" rel="noopener noreferrer">
                    <div class="fixed-card">
                        <div class="card-header">
                            <div class="card-icon img-box">
                                <img src="icon/E4.png">
                            </div>
                            <h3>Salhack</h3>
                        </div>
                        <div class="card-content">
                            <p>水晶PVP客户端<br />不知名客户端 冷门 国外 <停更></p>
                        </div>
                    </div>
                </a>
				
				<a href="https://www.mc-mod.net/skillclient/" class="card-link" target="_blank" rel="noopener noreferrer">
                    <div class="fixed-card">
                        <div class="card-header">
                            <div class="card-icon img-box">
                                <img src="icon/E4.png">
                            </div>
                            <h3>Skill</h3>
                        </div>
                        <div class="card-content">
                            <p>水晶PVP客户端<br />新客户端的垫脚石 冷门 国外<消失></p>
                        </div>
                    </div>
                </a>
				
				<a href="https://kamiblue.org/" class="card-link" target="_blank" rel="noopener noreferrer">
                    <div class="fixed-card">
                        <div class="card-header">
                            <div class="card-icon img-box">
                                <img src="icon/KamiBlue.png">
                            </div>
                            <h3>KamiBlue</h3>
                        </div>
                        <div class="card-content">
                            <p>水晶PVP客户端<br />美丽的多模块客户端 日本<停更></p>
                        </div>
                    </div>
                </a>
				
				</div>
        </section>
		
		
		<!--                1.16.5                 -->
		<section id="Free-Client-1.16.5">
            <h2 class="section-title">免费,开源1.16.5客户端</h2>
            <div class="card-container">
                <a href="https://github.com/zeroeightysix/KAMI/" class="card-link" target="_blank" rel="noopener noreferrer">
                    <div class="fixed-card">
                        <div class="card-header">
                            <div class="card-icon img-box">
                                <img src="icon/KamiBlue.png">
                            </div>
                            <h3>Kamiblue</h3>
                        </div>
                        <div class="card-content">
                            <p>水晶PVP客户端<br />Kami在高版本的分支 <停更></p>
                        </div>
                    </div>
                </a>
				
				<a href="https://impactclient.net/" class="card-link" target="_blank" rel="noopener noreferrer">
                    <div class="fixed-card">
                        <div class="card-header">
                            <div class="card-icon img-box">
                                <img src="icon/Impact.png">
                            </div>
                            <h3>Impact</h3>
                        </div>
                        <div class="card-content">
                            <p>水晶PVP客户端<br />逝去的强大客户端 <停更></p>
                        </div>
                    </div>
                </a>
				
				<a href="https://inertiaclient.com/" class="card-link" target="_blank" rel="noopener noreferrer">
                    <div class="fixed-card">
                        <div class="card-header">
                            <div class="card-icon img-box">
                                <img src="icon/Inertia.png">
                            </div>
                            <h3>Inertia</h3>
                        </div>
                        <div class="card-content">
                            <p>水晶PVP客户端<br />在21年使用Inertia在2b2tPVP... <停更></p>
                        </div>
                    </div>
                </a>
				
				</div>
				<div class="card-container">

				
				
				</div>
				
        </section>

			<section id="Paid-Client">
            <h2 class="section-title">付费客户端</h2>
            <div class="card-container">
                <a href="https://mioclient.me/" class="card-link" target="_blank" rel="noopener noreferrer">
                    <div class="fixed-card">
                        <div class="card-header">
                            <div class="card-icon img-box">
                                <img src="icon/Mio.png">
                            </div>
                            <h3>Mio</h3>
                        </div>
                        <div class="card-content">
                            <p>高版本水晶PVP客户端 20＄<br />不了解 只是顺带整理一下</p>
                        </div>
                    </div>
                </a>
				
				<a href="https://www.futureclient.net/" class="card-link" target="_blank" rel="noopener noreferrer">
                    <div class="fixed-card">
                        <div class="card-header">
                            <div class="card-icon img-box">
                                <img src="icon/Future.png">
                            </div>
                            <h3>Future</h3>
                        </div>
                        <div class="card-content">
                            <p>高版本水晶PVP客户端 19.99＄<br />不了解 只是顺带整理一下</p>
                        </div>
                    </div>
                </a>
				
				
				
				</div>
				<div class="card-container">

				
				
				</div>
				
        </section>




        <!--  -->
        <section id="Free-inject">
            <h2 class="section-title">免费热注入</h2>
            <div class="card-container">
                <!--  -->
                <a href="https://doomsdayclient.com/" class="card-link" target="_blank" rel="noopener noreferrer">
                    <div class="fixed-card">
                        <div class="card-header">
                            <div class="card-icon img-box">
                                <img src="icon/DD.png">
                            </div>
                            <h3>DoomsDay</h3>
                        </div>
                        <div class="card-content">
                            <p>轻量免费热注入 支持1.7.4至最新版本<br />兼容性强 模块40+ 国外</p>
                        </div>
                    </div>
                </a>

                <!--  -->
                <a href="https://github.com/yapeteam/YolBi_Lite_Recode" class="card-link" target="_blank" rel="noopener noreferrer">
                    <div class="fixed-card">
                        <div class="card-header">
                            <div class="card-icon img-box">
                                <img src="icon/YolBi_Lite.png">
                            </div>
                            <h3>YolBi Lite Recode</h3>
                        </div>
                        <div class="card-content">
                            <p>免费开源热注入 模块少<br />最新版本需要自己编译 国内</p>
                        </div>
                    </div>
                </a>
            </div>
			
			
        </section>
		
		<section id="Paid-inject">
            <h2 class="section-title">付费热注入</h2>
            <div class="card-container">
                <!--  -->
                <a href="vape.gg" class="card-link" target="_blank" rel="noopener noreferrer">
                    <div class="fixed-card">
                        <div class="card-header">
                            <div class="card-icon img-box">
                                <img src="icon/VAPEV4.png">
                            </div>
                            <h3>VAPE V4</h3>
                        </div>
                        <div class="card-content">
                            <p>低版本老牌安全客户端 34＄<br />高性价比 兼容性一般 对于预算不足的作弊者友好 注入和进入官网需要VPN 美国</p>
                        </div>
                    </div>
                </a>

                <!-- 其他热注入示例 -->
                <a href="https://drip.gg" class="card-link" target="_blank" rel="noopener noreferrer">
                    <div class="fixed-card">
                        <div class="card-header">
                            <div class="card-icon img-box">
                                <img src="icon/DripLite.png">
                            </div>
                            <h3>Drip Lite</h3>
                        </div>
                        <div class="card-content">
                            <p>全版本老牌付费幽灵客户端 80＄<br />按照官方指南可以绕过所有查端软件 网页Gui 绕OBS 美丽 模块42 美国</p>
                        </div>
                    </div>
                </a>
				
				
            </div>
			
			<div class="card-container">
			<a href="https://github.com/yapeteam/YolBi_Lite_Recode" class="card-link" target="_blank" rel="noopener noreferrer">
                    <div class="fixed-card">
                        <div class="card-header">
                            <div class="card-icon img-box">
                                <img src="icon/Entropy.png">
                            </div>
                            <h3>Entropy</h3>
                        </div>
                        <div class="card-content">
                            <p>幽灵客户端 10＄每月/50＄终身<br />高质量 绕过查端软件 兼容性好 外置Gui</p>
                        </div>
                    </div>
                </a>
				
				<a href="https://dreamclient.xyz/" class="card-link" target="_blank" rel="noopener noreferrer">
                    <div class="fixed-card">
                        <div class="card-header">
                            <div class="card-icon img-box">
                                <img src="icon/Dream.png">
                            </div>
                            <h3>Dream</h3>
                        </div>
                        <div class="card-content">
                            <p>幽灵客户端 6.99＄每月/30＄终身<br />性价比 绕过查端软件 兼容性好 网页Gui</p>
                        </div>
                    </div>
                </a>
				
				<a href="https://slinky.gg/" class="card-link" target="_blank" rel="noopener noreferrer">
                    <div class="fixed-card">
                        <div class="card-header">
                            <div class="card-icon img-box">
                                <img src="icon/slinky.png">
                            </div>
                            <h3>Slinky</h3>
                        </div>
                        <div class="card-content">
                            <p>多模块客户端 15€ 1个月/30€ 3个月/75€ 1年<br />高于VAPEV4 多个模块 兼容性好</p>
                        </div>
                    </div>
                </a>
				
			</div>
			
			<div class="card-container">
			
			<a href="https://karma.rip/" class="card-link" target="_blank" rel="noopener noreferrer">
                    <div class="fixed-card">
                        <div class="card-header">
                            <div class="card-icon img-box">
                                <img src="icon/Karma.png">
                            </div>
                            <h3>Karma</h3>
                        </div>
                        <div class="card-content">
                            <p>多模块客户端 9.99＄每月<br />绕过查端软件 兼容性好 C++ 外置Gui</p>
                        </div>
                    </div>
                </a>
			
			<a href="https://www.breeze.rip/" class="card-link" target="_blank" rel="noopener noreferrer">
                   <div class="fixed-card">
                       <div class="card-header">
                           <div class="card-icon img-box">
                               <img src="icon/Breeze.png">
                            </div>
                            <h3>Breeze</h3>
                        </div>
                        <div class="card-content">
                            <p>1.8.9Hyp暴力客户端 19.99＄<br />24.99＄普通版本终身 34.99＄高级版本 7.49＄每月</p>
                        </div>
                    </div>
                </a>
			
			
			</div>
			
			
        </section>
		
		<section id="PVP-Client">
            <h2 class="section-title">合法PVP客户端</h2>
            <div class="card-container">
                <a href="https://www.lunarclient.com/" class="card-link" target="_blank" rel="noopener noreferrer">
                    <div class="fixed-card">
                        <div class="card-header">
                            <div class="card-icon img-box">
                                <img src="icon/Lunar.png">
                            </div>
                            <h3>Lunar</h3>
                        </div>
                        <div class="card-content">
                            <p>高FPSPVP客户端<br />高度自定义HUD 稳定更新</p>
                        </div>
                    </div>
                </a>
				
				<a href="https://www.badlion.net/" class="card-link" target="_blank" rel="noopener noreferrer">
                    <div class="fixed-card">
                        <div class="card-header">
                            <div class="card-icon img-box">
                                <img src="icon/Badlion.png">
                            </div>
                            <h3>badlion</h3>
                        </div>
                        <div class="card-content">
                            <p>即将死亡的客户端 Lunar收购了Badlion<br />离Lunar太近 离天堂太远 相比于Lunar优化差了一点</p>
                        </div>
                    </div>
                </a>
				
				<a href="https://www.labymod.net/download" class="card-link" target="_blank" rel="noopener noreferrer">
                    <div class="fixed-card">
                        <div class="card-header">
                            <div class="card-icon img-box">
                                <img src="icon/LabyMod.png">
                            </div>
                            <h3>LabyMod</h3>
                        </div>
                        <div class="card-content">
                            <p>与Badlion同等优化的客户端<br />美丽的启动界面 一般的优化</p>
                        </div>
                    </div>
                </a>
				
				
				
				</div>
				<div class="card-container">
				<a href="https://cm-pack.pl/zh/download" class="card-link" target="_blank" rel="noopener noreferrer">
                    <div class="fixed-card">
                        <div class="card-header">
                            <div class="card-icon img-box">
                                <img src="icon/CM.png">
                            </div>
                            <h3>CM</h3>
                        </div>
                        <div class="card-content">
                            <p>良好动画的客户端<br />FPS优秀的准星偏移客户端</p>
                        </div>
                    </div>
                </a>
				
				<a href="https://alpineclient.com/" class="card-link" target="_blank" rel="noopener noreferrer">
                    <div class="fixed-card">
                        <div class="card-header">
                            <div class="card-icon img-box">
                                <img src="icon/Alpine.png">
                            </div>
                            <h3>Alpine</h3>
                        </div>
                        <div class="card-content">
                            <p>不知名的客户端<br />FPS高但渲染差劲的客户端</p>
                        </div>
                    </div>
                </a>
				
				
				</div>
        </section>
		
		
    </main>
	
	
	
</body>
</html>
