<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>听心格爱生命之树 - 情绪自查工具</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'PingFang SC', 'Hiragino Sans GB', 'Microsoft YaHei', sans-serif;
            background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
            min-height: 100vh;
            padding: 20px;
            color: #333;
        }
        
        .container {
            max-width: 700px;
            margin: 0 auto;
            background: white;
            border-radius: 20px;
            box-shadow: 0 10px 40px rgba(0,0,0,0.1);
            overflow: hidden;
        }
        
        .header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 30px;
            text-align: center;
        }

        /* LOGO样式调整：尺寸加大一倍 */
        .logo-img {
            width: 220px; /* 从110px调整为220px */
            max-width: 90%; /* 防止在超小手机屏幕溢出 */
            height: auto; 
            border-radius: 8px; 
            border: 3px solid rgba(255,255,255,0.3);
            margin-bottom: 15px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.2);
            background: white;
        }
        
        .header h1 {
            font-size: 24px;
            margin-bottom: 10px;
            font-weight: bold;
        }
        
        .header p {
            font-size: 15px; /* 稍微调大了一点 */
            opacity: 0.95;
            font-weight: 500;
        }
        
        .progress-bar {
            display: flex;
            justify-content: center;
            padding: 20px;
            background: #f8f9fa;
            gap: 10px;
            flex-wrap: wrap;
        }
        
        .step-indicator {
            width: 30px;
            height: 30px;
            border-radius: 50%;
            background: #e0e0e0;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 12px;
            font-weight: bold;
            color: #999;
            transition: all 0.3s;
        }
        
        .step-indicator.active {
            background: #667eea;
            color: white;
            transform: scale(1.1);
        }
        
        .step-indicator.completed {
            background: #48bb78;
            color: white;
        }
        
        .content {
            padding: 30px;
            min-height: 400px;
        }
        
        .step-title {
            font-size: 20px;
            color: #667eea;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .step-desc {
            color: #666;
            margin-bottom: 25px;
            font-size: 15px;
            line-height: 1.6;
            padding: 15px;
            background: #f0f4ff;
            border-radius: 8px;
            border-left: 4px solid #667eea;
        }

        /* 强调选择类型的样式 */
        .select-emphasis {
            font-size: 18px;
            font-weight: bold;
            color: #e65100;
            margin-right: 5px;
        }
        
        .category-section {
            margin-bottom: 25px;
            border: 1px solid #e0e0e0;
            border-radius: 12px;
            overflow: hidden;
        }
        
        .category-header {
            background: #f8f9fa;
            padding: 15px 20px;
            font-weight: 600;
            color: #5d4e37;
            font-size: 16px;
            border-bottom: 1px solid #e0e0e0;
        }
        
        .items-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 0;
        }
        
        .item {
            padding: 12px 15px;
            border-bottom: 1px solid #f0f0f0;
            border-right: 1px solid #f0f0f0;
            cursor: pointer;
            transition: all 0.2s;
            display: flex;
            align-items: center;
            gap: 10px;
            font-size: 14px;
        }
        
        .item:hover {
            background: #f8f9ff;
        }
        
        .item.selected {
            background: #667eea;
            color: white;
        }
        
        .item-checkbox {
            width: 18px;
            height: 18px;
            border: 2px solid currentColor;
            border-radius: 4px;
            flex-shrink: 0;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 12px;
        }
        
        .item.selected .item-checkbox::after {
            content: '✓';
            font-weight: bold;
        }
        
        .item-text {
            flex: 1;
            line-height: 1.4;
        }
        
        .single-select .item-checkbox {
            border-radius: 50%;
        }
        
        .single-select .item.selected .item-checkbox::after {
            content: '';
            width: 8px;
            height: 8px;
            background: white;
            border-radius: 50%;
        }
        
        .input-group {
            margin-bottom: 20px;
        }
        
        .input-group label {
            display: block;
            margin-bottom: 8px;
            color: #555;
            font-weight: 500;
        }
        
        .input-group input {
            width: 100%;
            padding: 12px 15px;
            border: 2px solid #e0e0e0;
            border-radius: 10px;
            font-size: 16px;
            transition: border-color 0.3s;
        }
        
        .input-group input:focus {
            outline: none;
            border-color: #667eea;
        }
        
        .btn-group {
            display: flex;
            gap: 15px;
            margin-top: 30px;
            position: sticky;
            bottom: 0;
            background: white;
            padding: 20px 0;
            border-top: 1px solid #eee;
        }
        
        .btn {
            flex: 1;
            padding: 15px;
            border: none;
            border-radius: 10px;
            font-size: 16px;
            cursor: pointer;
            transition: all 0.3s;
            font-weight: 500;
        }
        
        .btn-primary {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
        }
        
        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 20px rgba(102, 126, 234, 0.4);
        }
        
        .btn-secondary {
            background: #f0f0f0;
            color: #666;
        }
        
        .btn-secondary:hover {
            background: #e0e0e0;
        }
        
        .btn:disabled {
            opacity: 0.5;
            cursor: not-allowed;
            transform: none;
        }
        
        .selection-summary {
            background: #e8f5e9;
            border: 1px solid #81c784;
            border-radius: 8px;
            padding: 12px;
            margin-bottom: 20px;
            font-size: 14px;
            color: #2e7d32;
        }
        
        /* 首页计数器样式 */
        .counter-box {
            background: linear-gradient(135deg, #fff9e6 0%, #ffe4b5 100%);
            border: 2px solid #ffd700;
            border-radius: 12px;
            padding: 20px;
            text-align: center;
            margin-bottom: 25px;
            position: relative;
            overflow: hidden;
        }
        
        .counter-box::before {
            content: '✨';
            position: absolute;
            top: 10px;
            left: 15px;
            font-size: 20px;
            opacity: 0.3;
        }
        
        .counter-box::after {
            content: '✨';
            position: absolute;
            bottom: 10px;
            right: 15px;
            font-size: 20px;
            opacity: 0.3;
        }
        
        /* 调整后的计数器样式 */
        .counter-label-large {
            font-size: 20px;
            font-weight: bold;
            color: #8d6e63;
            margin-bottom: 5px;
        }

        .counter-number {
            font-size: 42px; /* 加大 */
            font-weight: 900; /* 加粗 */
            color: #e65100;
            margin: 10px 0;
            font-family: 'Courier New', monospace;
            letter-spacing: 2px;
            text-shadow: 1px 1px 0px rgba(255,255,255,0.5);
        }
        
        .counter-text {
            color: #8d6e63;
            font-size: 15px;
            line-height: 1.6;
        }
        
        .counter-highlight {
            color: #e65100;
            font-weight: 600;
        }
        
        /* 报告样式 */
        .report-full {
            background: linear-gradient(135deg, #faf8f5 0%, #f5f0e8 100%);
            border-radius: 15px;
            padding: 25px;
            margin-top: 20px;
        }
        
        .report-header-full {
            text-align: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 2px solid #e0d5c5;
        }
        
        .report-title-full {
            font-size: 22px;
            color: #5d4e37;
            font-weight: bold;
            margin-bottom: 5px;
        }
        
        .report-date-full {
            color: #8b7355;
            font-size: 13px;
        }
        
        .report-path {
            display: flex;
            flex-direction: column;
            gap: 15px;
        }
        
        .path-card {
            background: white;
            border-radius: 12px;
            padding: 18px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.06);
            border-left: 4px solid;
        }
        
        .path-card.sky { border-left-color: #64b5f6; }
        .path-card.crown { border-left-color: #81c784; }
        .path-card.trunk { border-left-color: #ffb74d; }
        .path-card.root { border-left-color: #f06292; }
        .path-card.soil { border-left-color: #a1887f; }
        
        .path-card-header {
            display: flex;
            align-items: center;
            gap: 10px;
            margin-bottom: 12px;
            font-weight: 600;
            color: #5d4e37;
            font-size: 15px;
        }
        
        .path-card-icon {
            font-size: 20px;
        }
        
        .path-card-content {
            color: #5d4e37;
            font-size: 14px;
            line-height: 1.8;
        }
        
        .path-card-category {
            font-weight: 600;
            color: #667eea;
            margin-bottom: 8px;
            padding-bottom: 8px;
            border-bottom: 1px dashed #e0e0e0;
        }
        
        .path-card-items {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
        }
        
        .item-tag {
            background: #f5f0e8;
            color: #5d4e37;
            padding: 4px 12px;
            border-radius: 15px;
            font-size: 13px;
            border: 1px solid #e0d5c5;
        }
        
        .path-arrow {
            text-align: center;
            color: #c9b896;
            font-size: 24px;
            margin: 5px 0;
        }
        
        /* 咨询区域 */
        .consult-section-full {
            margin-top: 20px;
            background: white;
            border-radius: 12px;
            padding: 20px;
            text-align: center;
            box-shadow: 0 2px 10px rgba(0,0,0,0.06);
            border: 2px dashed #c9b896;
        }
        
        .consult-title-full {
            font-size: 16px;
            color: #5d4e37;
            font-weight: 600;
            margin-bottom: 15px;
        }
        
        .consult-content-full {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 20px;
            flex-wrap: wrap;
        }
        
        .qr-image {
            width: 100px;
            height: 100px;
            border-radius: 8px;
            overflow: hidden;
            box-shadow: 0 2px 8px rgba(0,0,0,0.1);
        }
        
        .qr-image img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }
        
        .consult-info-full {
            text-align: left;
            font-size: 14px;
            color: #666;
            line-height: 1.8;
        }
        
        .consult-info-full strong {
            color: #667eea;
            font-size: 16px;
        }
        
        .consult-btn-full {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 10px 25px;
            border-radius: 25px;
            font-size: 14px;
            margin-top: 10px;
            display: inline-block;
            font-weight: 500;
        }
        
        .report-footer-full {
            margin-top: 20px;
            text-align: center;
            padding: 20px;
            background: #5d4e37;
            color: #f5f0e8;
            border-radius: 12px;
            font-size: 14px;
            line-height: 1.8;
            font-weight: 500;
        }
        
        .screenshot-tip-full {
            background: #fff3cd;
            border: 1px solid #ffeaa7;
            color: #856404;
            padding: 15px;
            border-radius: 8px;
            margin-bottom: 20px;
            text-align: center;
            font-size: 14px;
            font-weight: 500;
        }
        
        .hidden { display: none; }
        .fade-in { animation: fadeIn 0.5s ease-in; }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        @media (max-width: 600px) {
            body { padding: 10px; }
            .content { padding: 20px; }
            .report-full { padding: 20px; }
            .counter-number { font-size: 36px; }
            .path-card { padding: 15px; }
            .qr-image { width: 80px; height: 80px; }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <img src="https://raw.githubusercontent.com/txga01Lwz/qr-code/main/txga2.png" alt="听心格爱" class="logo-img">
            <h1>🌳 听心格爱生命之树</h1>
            <p>真正的爱自己就是“看见”真实的自己</p>
        </div>
        
        <div class="progress-bar" id="progressBar">
            <div class="step-indicator active" data-step="0">1</div>
            <div class="step-indicator" data-step="1">2</div>
            <div class="step-indicator" data-step="2">3</div>
            <div class="step-indicator" data-step="3">4</div>
            <div class="step-indicator" data-step="4">5</div>
            <div class="step-indicator" data-step="5">6</div>
            <div class="step-indicator" data-step="6">7</div>
        </div>
        
        <div class="content" id="content"></div>
    </div>

    <script>
        // 预设的50组数字，30万-50万之间
        const userCounters = [
            356477, 356478, 356479, 356480, 356481,
            356482, 356483, 356484, 356485, 356486,
            356487, 356488, 356489, 356490, 356491,
            356492, 356493, 356494, 356495, 356496,
            356497, 356498, 356499, 356500, 356501,
            356502, 356503, 356504, 356505, 356506,
            356507, 356508, 356509, 356510, 356511,
            356512, 356513, 356514, 356515, 356516,
            356517, 356518, 356519, 356520, 356521,
            356522, 356523, 356524, 356525, 356526
        ];
        
        // 随机选择一个基础数字
        const baseCounter = userCounters[Math.floor(Math.random() * userCounters.length)];
        
        const steps = [
            {
                id: 'welcome',
                title: '🌟 开启您的觉醒之路',
                subtitle: '（全程约三分钟）',
                desc: '',
                type: 'welcome',
                counter: baseCounter
            },
            {
                id: 'info',
                title: '📝 基本信息',
                desc: '请填写您的基本信息，这将出现在您的个人报告中',
                type: 'form',
                fields: [
                    { id: 'name', label: '您的称呼', placeholder: '例如：小明', required: true },
                    { id: 'gender', label: '性别', placeholder: '男/女', required: true },
                    { id: 'age', label: '年龄', placeholder: '例如：28', required: true },
                    { id: 'phone', label: '联系电话', placeholder: '用于标识您的报告', required: true }
                ]
            },
            {
                id: 'sky',
                title: '🌤️ 天空 - 发生了什么事',
                desc: '<span class="select-emphasis">【单选】</span>请选择一件最近让您情绪波动最强烈的具体事件：',
                type: 'single',
                categories: [
                    { name: '感情关系类', items: ['对方冷淡', '不回消息', '回得敷衍', '态度变了', '不解释', '不耐烦', '和别人走得近', '出现异性', '暧昧', '隐瞒事情', '说谎', '吵架', '冷战', '被忽略', '被比较', '被嫌弃', '不陪我', '不被优先选择', '被放在后面'] },
                    { name: '现实工作金钱类', items: ['没钱', '负债', '收入下降', '工作不顺', '被批评', '被否定能力', '被裁员', '升职失败', '项目失败', '压力大', '被取代', '没前途感', '做得再多也没人看见', '努力没回报', '破产'] },
                    { name: '家庭成长类', items: ['父母不理解', '被管太多', '被否定', '被打压', '偏心别人', '要求太高', '不被尊重', '不被支持', '不被倾听', '被控制', '无法自主'] },
                    { name: '身体生活状态类', items: ['紧张', '强迫症', '厌食症', '生病', '体力变差', '状态不好', '变胖变老', '外貌变化', '容易累', '失眠', '身体透支'] },
                    { name: '理想现实落差类', items: ['梦想没实现', '活成不想要的样子', '和别人差距变大', '越来越普通', '年纪焦虑', '没方向', '迷茫', '没有成就感'] }
                ]
            },
            {
                id: 'crown',
                title: '🌳 树冠 - 下意识做了什么',
                desc: '<span class="select-emphasis">【多选】</span>请选择您当时几乎来不及思考就做出来的反应：',
                type: 'multiple',
                categories: [
                    { name: '控制型反应', items: ['不停追问', '反复确认', '查手机', '盯着对方', '一定要说清楚', '非要答案', '不让对方躲'] },
                    { name: '讨好型反应', items: ['忍着不说', '委屈自己', '假装没事', '一直让步', '什么都答应', '不敢提要求', '过度付出', '怕惹事'] },
                    { name: '回避型反应', items: ['沉默', '装没事', '消失', '冷处理', '不解释', '逃避话题', '不回应', '切断联系'] },
                    { name: '攻击型反应', items: ['阴阳怪气', '讽刺', '指责', '吵架', '翻旧账', '发脾气', '说狠话', '冷暴力'] },
                    { name: '证明型反应', items: ['拼命解释', '争对错', '不服软', '讲道理', '坚持自己没错', '反复辩解'] },
                    { name: '内耗型反应', items: ['反复想', '骂自己', '后悔', '纠结', '脑补', '睡不着', '消耗自己', '反复复盘'] }
                ]
            },
            {
                id: 'trunk',
                title: '🪵 树干 - 心里的真实感受',
                desc: '<span class="select-emphasis">【多选】</span>请选择您内心真正的情绪和心理感受：',
                type: 'multiple',
                categories: [
                    { name: '不安害怕类', items: ['心慌', '不踏实', '害怕', '紧张', '担心', '没安全感', '怕失去', '恐慌', '焦虑'] },
                    { name: '委屈失落类', items: ['委屈', '难过', '失望', '孤独', '空虚', '被忽视', '被抛下感', '无助'] },
                    { name: '生气不满类', items: ['生气', '烦', '憋屈', '不爽', '怨', '火大', '被冒犯', '不公平感'] },
                    { name: '否定自己类', items: ['自卑', '觉得自己没用', '觉得自己很差', '怀疑自己', '没价值感', '觉得配不上', '羞愧', '自责'] },
                    { name: '身体反应类', items: ['失眠', '心累', '没力气', '胃不舒服', '头疼', '胸闷', '提不起精神', '情绪低落'] }
                ]
            },
            {
                id: 'root',
                title: '🌱 树根 - 真正想要什么',
                desc: '<span class="select-emphasis">【多选】</span>请选择您情绪背后的真实需求：',
                type: 'multiple',
                categories: [
                    { name: '安全感需求', items: ['想确定你不会走', '想安心', '想稳定', '不想被抛弃', '不想再受伤', '想有依靠'] },
                    { name: '被爱需求', items: ['想被珍惜', '被在乎', '想被选择', '想被放第一', '想被疼', '想被偏爱'] },
                    { name: '被理解需求', items: ['被听见', '被懂', '被共情', '想有人站在我这边', '想被认真对待'] },
                    { name: '被认可需求', items: ['想被肯定', '被夸', '被承认价值', '被尊重', '被看见努力', '被需要'] },
                    { name: '位置感需求', items: ['我重要吗', '我算什么', '我排第几', '我有没有地位', '有没有分量', '我是不是可有可无'] },
                    { name: '掌控感需求', items: ['不想失控', '不想被摆布', '想掌握主动', '有边界', '想有选择权'] },
                    { name: '存在感需求', items: ['我是不是有意义', '我是不是被记得', '我是不是重要的人'] }
                ]
            },
            {
                id: 'soil',
                title: '🪨 土壤 - 观念的来源',
                desc: '<span class="select-emphasis">【多选】</span>请选择形成您现在模式的成长背景：',
                type: 'multiple',
                categories: [
                    { name: '家庭经历', items: ['父母冷漠', '爱打压', '要求高', '很少夸人', '偏心', '控制强', '情绪不稳定', '缺乏陪伴', '忽视情绪'] },
                    { name: '感情经历', items: ['被甩过', '背叛', '忽略', '骗过', '伤很深', '比较', '替代', '被放弃'] },
                    { name: '成长经历', items: ['常被否定', '常被比较', '要懂事', '要听话', '要争气', '不能丢脸', '不能犯错', '不能失败'] },
                    { name: '长期状态', items: ['长期委屈', '压抑', '讨好', '独扛', '没人懂', '缺爱', '长期孤独'] },
                    { name: '环境影响', items: ['竞争', '压力大', '缺乏安全', '资源匮乏', '支持弱', '情绪不被重视'] },
                    { name: '文化观念影响', items: ['要优秀才有价值', '要成功才被尊重', '不能示弱', '不能失败', '情绪是没用的'] }
                ]
            }
        ];

        let currentStep = 0;
        let userData = { name: '', gender: '', age: '', phone: '', answers: {} };
        let userCounterNumber = baseCounter;

        function renderStep() {
            const step = steps[currentStep];
            const content = document.getElementById('content');
            
            // 更新进度条（欢迎页不显示进度）
            if (step.type !== 'welcome') {
                document.getElementById('progressBar').style.display = 'flex';
                document.querySelectorAll('.step-indicator').forEach((ind, idx) => {
                    ind.classList.remove('active', 'completed');
                    const stepIndex = currentStep - 1; // 减去欢迎页
                    if (idx < stepIndex) ind.classList.add('completed');
                    else if (idx === stepIndex) ind.classList.add('active');
                });
            } else {
                document.getElementById('progressBar').style.display = 'none';
            }

            let html = `<div class="fade-in">`;

            if (step.type === 'welcome') {
                html += `
                    <div class="counter-box">
                        <div class="counter-label-large">已有</div>
                        <div class="counter-number" id="counterNum">${step.counter.toLocaleString()}</div>
                        <div class="counter-text">
                            人找到自己的<span class="counter-highlight">生命之树</span><br>
                            您是第 <span class="counter-highlight" id="userNum">${(step.counter + 1).toLocaleString()}</span> 位探索者
                        </div>
                    </div>
                    <h2 class="step-title" style="text-align: center; justify-content: center; flex-direction: column; gap: 5px;">
                        ${step.title}
                        <span style="font-size: 16px; font-weight: normal; color: #666;">${step.subtitle}</span>
                    </h2>
                    <p class="step-desc" style="text-align: center; background: transparent; border: none;">
                        这不是评判你的工具，而是陪你看懂自己的地图<br>
                        当事情发生时，你为什么会这样反应？<br>
                        你心里真正缺的是什么？<br>
                        这些感受又从哪里来？
                    </p>
                    <div style="text-align: center; margin: 30px 0;">
                        <div style="background: #f8f9fa; border-radius: 12px; padding: 20px; margin: 20px 0; text-align: left;">
                            <p style="color: #666; font-size: 14px; line-height: 2; margin: 0;">
                                🌤️ <strong>天空</strong>：发生了什么事件<br>
                                🌳 <strong>树冠</strong>：你下意识做了什么<br>
                                🪵 <strong>树干</strong>：你的真实感受<br>
                                🌱 <strong>树根</strong>：你真正想要什么<br>
                                🪨 <strong>土壤</strong>：这些模式从哪里来
                            </p>
                        </div>
                    </div>
                `;
            } else {
                html += `<h2 class="step-title">${step.title}</h2><p class="step-desc">${step.desc}</p>`;

                if (step.type === 'form') {
                    html += `<div style="max-width: 400px; margin: 0 auto;">`;
                    step.fields.forEach(field => {
                        const value = userData[field.id] || '';
                        html += `<div class="input-group"><label>${field.label}${field.required ? ' *' : ''}</label><input type="text" id="${field.id}" value="${value}" placeholder="${field.placeholder}" onchange="updateFormData('${field.id}', this.value)"></div>`;
                    });
                    html += `</div>`;
                } else {
                    const currentSelection = userData.answers[step.id] || [];
                    if (currentSelection.length > 0) {
                        html += `<div class="selection-summary"><strong>已选择 ${currentSelection.length} 项：</strong>${currentSelection.join('、')}</div>`;
                    }

                    const selectClass = step.type === 'single' ? 'single-select' : '';
                    html += `<div class="${selectClass}">`;
                    
                    step.categories.forEach(cat => {
                        html += `<div class="category-section"><div class="category-header">${cat.name}</div><div class="items-grid">`;
                        cat.items.forEach(item => {
                            const isSelected = currentSelection.includes(item);
                            html += `<div class="item ${isSelected ? 'selected' : ''}" onclick="toggleItem('${step.id}', '${item}', '${step.type}', '${cat.name}')"><div class="item-checkbox"></div><div class="item-text">${item}</div></div>`;
                        });
                        html += `</div></div>`;
                    });
                    html += `</div>`;
                }
            }

            html += `<div class="btn-group">`;
            if (currentStep > 0) html += `<button class="btn btn-secondary" onclick="prevStep()">← 上一步</button>`;
            else html += `<div></div>`;
            
            const isLast = currentStep === steps.length - 1;
            const btnText = isLast ? '生成报告 →' : (step.type === 'welcome' ? '开始探索 →' : '下一步 →');
            const btnAction = isLast ? 'generateReport()' : 'nextStep()';
            
            let canProceed = true;
            if (step.type === 'form') canProceed = userData.name && userData.phone && userData.gender && userData.age;
            else if (step.type === 'single') canProceed = (userData.answers[step.id] || []).length === 1;
            else if (step.type === 'multiple') canProceed = (userData.answers[step.id] || []).length > 0;
            
            html += `<button class="btn btn-primary" onclick="${btnAction}" ${!canProceed ? 'disabled' : ''}>${btnText}</button></div></div>`;
            content.innerHTML = html;
            
            // 如果是欢迎页，启动数字动画
            if (step.type === 'welcome') {
                animateCounter(step.counter);
            }
        }

        function animateCounter(target) {
            const duration = 2000;
            const start = target - 1000;
            const element = document.getElementById('counterNum');
            const startTime = performance.now();

            function update(currentTime) {
                const elapsed = currentTime - startTime;
                const progress = Math.min(elapsed / duration, 1);
                const easeProgress = 1 - Math.pow(1 - progress, 3);
                const current = Math.floor(start + (target - start) * easeProgress);
                
                if (element) element.textContent = current.toLocaleString();
                
                if (progress < 1) {
                    requestAnimationFrame(update);
                }
            }
            
            requestAnimationFrame(update);
        }

        function updateFormData(field, value) {
            userData[field] = value.trim();
            renderStep();
        }

        function toggleItem(stepId, item, type, categoryName) {
            if (!userData.answers[stepId]) userData.answers[stepId] = [];
            const current = userData.answers[stepId];
            
            if (type === 'single') {
                userData.answers[stepId] = [item];
                userData.answers[stepId + '_category'] = categoryName;
            } else {
                const index = current.indexOf(item);
                if (index > -1) current.splice(index, 1);
                else current.push(item);
            }
            renderStep();
        }

        function nextStep() {
            if (currentStep < steps.length - 1) {
                currentStep++;
                renderStep();
            }
        }

        function prevStep() {
            if (currentStep > 0) {
                currentStep--;
                renderStep();
            }
        }

        function generateReport() {
            // --------------------------------------------------------
            // 1. 准备要发送的数据 (适配 Web3Forms)
            // --------------------------------------------------------
            const reportData = {
                // 已替换为你提供的 QQ 邮箱 Access Key
                "access_key": "7a8f6fdd-2da0-4503-a64f-9fd4aac20362", 
                
                // 邮件标题
                "subject": "新的生命之树提交报告",
                
                // 用户填写的具体内容
                "姓名": userData.name,
                "性别": userData.gender,
                "年龄": userData.age,
                "电话": userData.phone,
                "天空(事件)": userData.answers.sky ? userData.answers.sky[0] : "",
                "树冠(反应)": userData.answers.crown ? userData.answers.crown.join(", ") : "",
                "树干(感受)": userData.answers.trunk ? userData.answers.trunk.join(", ") : "",
                "树根(需求)": userData.answers.root ? userData.answers.root.join(", ") : "",
                "土壤(来源)": userData.answers.soil ? userData.answers.soil.join(", ") : "",
                "提交时间": new Date().toLocaleString('zh-CN')
            };

            // --------------------------------------------------------
            // 2. 发送数据给 Web3Forms
            // --------------------------------------------------------
            fetch("https://api.web3forms.com/submit", {
                method: "POST",
                headers: {
                    "Content-Type": "application/json",
                    "Accept": "application/json"
                },
                body: JSON.stringify(reportData)
            })
            .then(async (response) => {
                if (response.status == 200) {
                    console.log("Web3Forms: 发送成功！");
                } else {
                    console.log("Web3Forms: 发送可能遇到问题", response);
                }
            })
            .catch(error => {
                console.log("Web3Forms: 发送出错", error);
            });

            // --------------------------------------------------------
            // 3. 生成报告页面 (保持不变的显示逻辑)
            // --------------------------------------------------------
            const content = document.getElementById('content');
            const date = new Date().toLocaleDateString('zh-CN');
            
            const skyItem = userData.answers.sky[0];
            const skyCategory = userData.answers.sky_category;
            const crownItems = userData.answers.crown || [];
            const trunkItems = userData.answers.trunk || [];
            const rootItems = userData.answers.root || [];
            const soilItems = userData.answers.soil || [];

            const html = `
                <div class="fade-in">
                    <div class="screenshot-tip-full">📸 请截图保存此报告 · 包含您的完整情绪路径与所有选择</div>
                    
                    <div class="report-full">
                        <div class="report-header-full">
                            <div class="report-title-full">🌳 ${userData.name}的生命之树</div>
                            <div class="report-date-full">听心格爱 · 第${userCounterNumber.toLocaleString()}位探索者 · ${date}</div>
                        </div>
                        
                        <div class="report-path">
                            <div class="path-card sky">
                                <div class="path-card-header">
                                    <span class="path-card-icon">🌤️</span>
                                    <span>天空 · 触发事件</span>
                                </div>
                                <div class="path-card-content">
                                    <div class="path-card-category">${skyCategory}</div>
                                    <div class="path-card-items">
                                        <span class="item-tag">${skyItem}</span>
                                    </div>
                                </div>
                            </div>
                            
                            <div class="path-arrow">↓</div>
                            
                            <div class="path-card crown">
                                <div class="path-card-header">
                                    <span class="path-card-icon">🌳</span>
                                    <span>树冠 · 自动反应</span>
                                </div>
                                <div class="path-card-content">
                                    <div class="path-card-items">
                                        ${crownItems.map(item => `<span class="item-tag">${item}</span>`).join('')}
                                    </div>
                                </div>
                            </div>
                            
                            <div class="path-arrow">↓</div>
                            
                            <div class="path-card trunk">
                                <div class="path-card-header">
                                    <span class="path-card-icon">🪵</span>
                                    <span>树干 · 真实感受</span>
                                </div>
                                <div class="path-card-content">
                                    <div class="path-card-items">
                                        ${trunkItems.map(item => `<span class="item-tag">${item}</span>`).join('')}
                                    </div>
                                </div>
                            </div>
                            
                            <div class="path-arrow">↓</div>
                            
                            <div class="path-card root">
                                <div class="path-card-header">
                                    <span class="path-card-icon">🌱</span>
                                    <span>树根 · 深层需求</span>
                                </div>
                                <div class="path-card-content">
                                    <div class="path-card-items">
                                        ${rootItems.map(item => `<span class="item-tag">${item}</span>`).join('')}
                                    </div>
                                </div>
                            </div>
                            
                            <div class="path-arrow">↓</div>
                            
                            <div class="path-card soil">
                                <div class="path-card-header">
                                    <span class="path-card-icon">🪨</span>
                                    <span>土壤 · 成长背景</span>
                                </div>
                                <div class="path-card-content">
                                    <div class="path-card-items">
                                        ${soilItems.map(item => `<span class="item-tag">${item}</span>`).join('')}
                                    </div>
                                </div>
                            </div>
                        </div>
                        
                        <div class="consult-section-full">
                            <div class="consult-title-full">💬 想更深入理解自己的情绪模式？</div>
                            <div class="consult-content-full">
                                <div class="qr-image">
                                    <img src="https://raw.githubusercontent.com/txga01Lwz/qr-code/main/qr.jpg" alt="微信二维码" onerror="this.style.display='none'; this.parentElement.innerHTML='<div style=\'width:100%;height:100%;display:flex;align-items:center;justify-content:center;background:#f0f0f0;color:#999;font-size:12px;\'>二维码</div>'">
                                </div>
                                <div class="consult-info-full">
                                    <div style="margin-top: 8px; color: #667eea; font-weight: 600;">
                                        一对一专业情绪解读<br>
                                        📱 微信/电话：13605734411
                                    </div>
                                    <div style="margin-top: 5px; font-size: 13px;">
                                        帮你看见模式背后的真相<br>
                                        如需帮助后台咨询
                                    </div>
                                    <div class="consult-btn-full">扫码预约咨询</div>
                                </div>
                            </div>
                        </div>
                        
                        <div class="report-footer-full">
                            截屏后根据（天空-树冠-树干-树根-土壤）<br>
                            依序找出它们彼此的关联点，<br>
                            这就是“我”背后那个真实的自己。<br>
                            <em>愿你看懂自己，温柔待己，因为你值得</em>
                        </div>
                    </div>
                    
                    <div class="btn-group" style="margin-top: 20px">
                        <button class="btn btn-secondary" onclick="location.reload()">🔄 重新开始</button>
                        <button class="btn btn-primary" onclick="alert('请截图保存上方完整报告')">📸 截图提示</button>
                    </div>
                </div>
            `;
            
            content.innerHTML = html;
            document.getElementById('progressBar').style.display = 'none';
        }

        renderStep();
    </script>
</body>
</html>
