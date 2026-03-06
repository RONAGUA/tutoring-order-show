[青蛙家教展示端.html](https://github.com/user-attachments/files/25789217/default.html)
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>家教订单展示系统 - 老师端</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: "Microsoft YaHei", sans-serif;
        }

        body {
            background-color: #f5f7fa;
            padding: 20px;
            line-height: 1.6;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
            background: white;
            border-radius: 12px;
            box-shadow: 0 2px 15px rgba(0,0,0,0.08);
            padding: 30px;
        }

        header {
            text-align: center;
            margin-bottom: 30px;
            padding-bottom: 20px;
            border-bottom: 2px solid #e8f4fd;
        }

        h1 {
            color: #2c3e50;
            margin-bottom: 10px;
            font-size: 28px;
        }

        .subtitle {
            color: #7f8c8d;
            font-size: 16px;
        }

        /* 筛选区域样式 */
        .filter-section {
            margin-bottom: 25px;
            padding: 20px;
            background-color: #f8f9fa;
            border-radius: 10px;
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            align-items: center;
        }

        .filter-item {
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .filter-label {
            color: #34495e;
            font-weight: 500;
        }

        select, .filter-checkbox {
            padding: 8px 12px;
            border: 1px solid #ddd;
            border-radius: 6px;
            font-size: 14px;
        }

        /* 分类标签样式 */
        .category-tabs {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }

        .category-tab {
            padding: 8px 20px;
            background-color: #e8f4fd;
            color: #3498db;
            border-radius: 20px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-weight: 500;
        }

        .category-tab.active {
            background-color: #3498db;
            color: white;
        }

        .category-tab:hover {
            background-color: #d6eaf8;
        }

        .category-tab.active:hover {
            background-color: #2980b9;
        }

        /* 订单列表样式 */
        .order-list {
            display: flex;
            flex-direction: column;
            gap: 20px;
        }

        .order-card {
            border: 1px solid #eee;
            border-radius: 10px;
            padding: 25px;
            background-color: white;
            position: relative;
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            overflow: hidden;
        }

        .order-card:hover {
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.08);
        }

        /* 标签样式 */
        .tag-container {
            position: absolute;
            top: 15px;
            right: 15px;
            display: flex;
            gap: 8px;
            flex-wrap: wrap;
        }

        .tag {
            padding: 4px 10px;
            border-radius: 4px;
            font-size: 12px;
            font-weight: 600;
            color: white;
        }

        .special-tag {
            background-color: #8e44ad;
        }

        .high-salary-tag {
            background-color: #e74c3c;
        }

        .discount-tag {
            background-color: #f39c12;
        }

        .online-tag {
            background-color: #2ecc71;
        }

        .fulltime-tag {
            background-color: #9b59b6;
        }

        .order-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 2px solid #f5f5f5;
        }

        .order-id {
            font-size: 20px;
            font-weight: 700;
            color: #2c3e50;
        }

        .action-buttons {
            display: flex;
            gap: 8px;
        }

        .copy-btn {
            padding: 8px 15px;
            background-color: #2ecc71;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 13px;
            font-weight: 500;
        }

        .copy-btn:hover {
            background-color: #27ae60;
        }

        .copy-address-btn {
            padding: 8px 15px;
            background-color: #9b59b6;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 13px;
            font-weight: 500;
        }

        .copy-address-btn:hover {
            background-color: #8e44ad;
        }

        /* 标准化订单信息布局 */
        .order-info {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            font-size: 15px;
        }

        .info-card {
            background-color: #f8f9fa;
            padding: 15px;
            border-radius: 8px;
            border: 1px solid #e8f4fd;
        }

        .info-card-title {
            font-size: 16px;
            font-weight: 600;
            color: #2c3e50;
            margin-bottom: 12px;
            padding-bottom: 8px;
            border-bottom: 2px solid #3498db;
        }

        .info-item {
            display: flex;
            margin-bottom: 8px;
            color: #34495e;
            flex-wrap: wrap;
        }

        .info-label {
            font-weight: 600;
            color: #2c3e50;
            min-width: 80px;
            display: inline-block;
        }

        .info-value {
            flex: 1;
            word-break: break-all;
        }

        .empty-value {
            color: #95a5a6;
            font-style: italic;
        }

        .no-order {
            text-align: center;
            padding: 50px;
            color: #7f8c8d;
            font-size: 18px;
        }

        /* 刷新按钮 */
        .refresh-btn {
            padding: 8px 15px;
            background-color: #3498db;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 13px;
            font-weight: 500;
            margin-left: 10px;
        }

        .refresh-btn:hover {
            background-color: #2980b9;
        }

        /* 响应式适配 */
        @media (max-width: 768px) {
            .filter-section {
                flex-direction: column;
                align-items: flex-start;
            }
            
            .order-header {
                flex-direction: column;
                align-items: flex-start;
                gap: 10px;
            }
            
            .action-buttons {
                width: 100%;
                justify-content: flex-start;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>家教订单展示系统 - 老师端</h1>
            <p class="subtitle">筛选订单、查看详情、复制信息 | 数据实时同步自管理端</p>
        </header>

        <!-- 筛选区域 -->
        <div class="filter-section">
            <div class="filter-item">
                <label class="filter-label">筛选地区：</label>
                <select id="areaFilter" onchange="filterOrders()">
                    <option value="all">全部地区</option>
                    <option value="松江区">松江区</option>
                    <option value="杨浦区">杨浦区</option>
                    <option value="虹口区">虹口区</option>
                    <option value="浦东新区">浦东新区</option>
                    <option value="黄浦区">黄浦区</option>
                    <option value="静安区">静安区</option>
                    <option value="徐汇区">徐汇区</option>
                    <option value="长宁区">长宁区</option>
                    <option value="普陀区">普陀区</option>
                    <option value="闵行区">闵行区</option>
                    <option value="宝山区">宝山区</option>
                    <option value="嘉定区">嘉定区</option>
                    <option value="金山区">金山区</option>
                    <option value="青浦区">青浦区</option>
                    <option value="奉贤区">奉贤区</option>
                    <option value="崇明区">崇明区</option>
                </select>
            </div>
            <div class="filter-item">
                <label class="filter-label">筛选科目：</label>
                <select id="subjectFilter" onchange="filterOrders()">
                    <option value="all">全部科目</option>
                    <option value="语文">语文</option>
                    <option value="数学">数学</option>
                    <option value="英语">英语</option>
                    <option value="物理">物理</option>
                    <option value="历史">历史</option>
                    <option value="化学">化学</option>
                    <option value="生物">生物</option>
                    <option value="地理">地理</option>
                    <option value="政治">政治</option>
                    <option value="计算机">计算机</option>
                    <option value="编程">编程</option>
                    <option value="special">特殊类（非预设科目/月薪单）</option>
                </select>
            </div>
            <div class="filter-item">
                <label class="filter-label">仅显示高薪订单：</label>
                <input type="checkbox" id="highSalaryFilter" class="filter-checkbox" onchange="filterOrders()">
            </div>
            <div class="filter-item">
                <label class="filter-label">仅显示折扣单：</label>
                <input type="checkbox" id="discountFilter" class="filter-checkbox" onchange="filterOrders()">
            </div>
            <div class="filter-item">
                <button class="refresh-btn" onclick="refreshOrders()">刷新订单</button>
            </div>
        </div>

        <!-- 分类标签 -->
        <div class="category-tabs">
            <div class="category-tab active" data-category="all">全部订单</div>
            <div class="category-tab" data-category="online">线上订单</div>
            <div class="category-tab" data-category="fulltime">专职在职订单</div>
            <div class="category-tab" data-category="area">地区订单</div>
            <div class="category-tab" data-category="discount">信息费折扣单</div>
            <div class="category-tab" data-category="special">特殊类订单</div>
        </div>

        <!-- 订单列表 -->
        <div class="order-list" id="orderList">
            <div class="no-order">加载中...请稍候</div>
        </div>
    </div>

    <script>
        // 全局订单数据
        let allOrders = [];
        let currentCategory = 'all';

        // 页面加载时读取本地存储的订单
        window.onload = function() {
            refreshOrders();
            bindCategoryTabs();
        };

        // 刷新订单（从本地存储重新读取）
        function refreshOrders() {
            const storedOrders = localStorage.getItem('tutoringOrders');
            if (storedOrders) {
                allOrders = JSON.parse(storedOrders);
                alert(`已加载最新订单数据，共${allOrders.length}条订单`);
            } else {
                allOrders = [];
                alert('暂无已保存的订单，请先在管理端录入并保存订单');
            }
            renderOrders();
        }

        // 绑定分类标签事件
        function bindCategoryTabs() {
            const tabs = document.querySelectorAll('.category-tab');
            tabs.forEach(tab => {
                tab.onclick = function() {
                    tabs.forEach(t => t.classList.remove('active'));
                    this.classList.add('active');
                    currentCategory = this.dataset.category;
                    renderOrders();
                };
            });
        }

        // 筛选订单
        function filterOrders() {
            renderOrders();
        }

        // 渲染展示端订单列表（仅展示+复制功能）
        function renderOrders() {
            const orderList = document.getElementById('orderList');
            const areaFilter = document.getElementById('areaFilter').value;
            const subjectFilter = document.getElementById('subjectFilter').value;
            const highSalaryFilter = document.getElementById('highSalaryFilter').checked;
            const discountFilter = document.getElementById('discountFilter').checked;

            // 筛选逻辑
            let filteredOrders = [...allOrders];

            // 按分类筛选
            if (currentCategory === 'online') {
                filteredOrders = filteredOrders.filter(order => order.type === 'online');
            } else if (currentCategory === 'fulltime') {
                filteredOrders = filteredOrders.filter(order => order.type === 'fulltime');
            } else if (currentCategory === 'area') {
                filteredOrders = filteredOrders.filter(order => order.type === 'area');
            } else if (currentCategory === 'discount') {
                filteredOrders = filteredOrders.filter(order => order.isDiscount);
            } else if (currentCategory === 'special') {
                filteredOrders = filteredOrders.filter(order => order.isSpecial);
            }

            // 按地区筛选
            if (areaFilter !== 'all') {
                filteredOrders = filteredOrders.filter(order => order.area === areaFilter);
            }

            // 按科目筛选
            if (subjectFilter !== 'all') {
                if (subjectFilter === 'special') {
                    filteredOrders = filteredOrders.filter(order => order.isSpecial);
                } else {
                    filteredOrders = filteredOrders.filter(order => order.subject.includes(subjectFilter));
                }
            }

            // 按高薪筛选
            if (highSalaryFilter) {
                filteredOrders = filteredOrders.filter(order => order.isHighSalary);
            }

            // 按折扣单筛选
            if (discountFilter) {
                filteredOrders = filteredOrders.filter(order => order.isDiscount);
            }

            // 渲染
            if (filteredOrders.length === 0) {
                orderList.innerHTML = '<div class="no-order">暂无符合条件的订单</div>';
                return;
            }

            let html = '';
            filteredOrders.forEach(order => {
                // 构建标签
                let tagsHtml = '';
                if (order.isSpecial) {
                    tagsHtml += '<span class="tag special-tag">特殊类</span>';
                }
                if (order.isHighSalary) {
                    tagsHtml += '<span class="tag high-salary-tag">高薪</span>';
                }
                if (order.isDiscount) {
                    tagsHtml += '<span class="tag discount-tag">折扣</span>';
                }
                if (order.type === 'online') {
                    tagsHtml += '<span class="tag online-tag">线上</span>';
                }
                if (order.type === 'fulltime') {
                    tagsHtml += '<span class="tag fulltime-tag">全职</span>';
                }

                // 格式化空值显示
                const formatValue = (value) => {
                    return value && value.trim() ? value : '<span class="empty-value">暂无信息</span>';
                };

                // 展示端布局（仅复制按钮）
                html += `
                <div class="order-card" data-id="${order.id}">
                    <div class="tag-container">${tagsHtml}</div>
                    <div class="order-header">
                        <div class="order-id">${order.id}</div>
                        <div class="action-buttons">
                            <button class="copy-btn" onclick="copyOrder('${order.id}')">复制本单</button>
                            <button class="copy-address-btn" onclick="copyAddress('${order.id}')">复制地址</button>
                        </div>
                    </div>
                    <div class="order-info">
                        <!-- 基础信息卡片 -->
                        <div class="info-card">
                            <div class="info-card-title">基础信息</div>
                            <div class="info-item">
                                <span class="info-label">地区：</span>
                                <span class="info-value">${formatValue(order.area)}</span>
                            </div>
                            <div class="info-item">
                                <span class="info-label">详细地址：</span>
                                <span class="info-value">${formatValue(order.address)}</span>
                            </div>
                            <div class="info-item">
                                <span class="info-label">学员年级：</span>
                                <span class="info-value">${formatValue(order.grade)}</span>
                            </div>
                            <div class="info-item">
                                <span class="info-label">学员性别：</span>
                                <span class="info-value">${formatValue(order.gender)}</span>
                            </div>
                            <div class="info-item">
                                <span class="info-label">辅导科目：</span>
                                <span class="info-value">${formatValue(order.subject)}</span>
                            </div>
                        </div>

                        <!-- 薪资时间卡片 -->
                        <div class="info-card">
                            <div class="info-card-title">薪资与时间</div>
                            <div class="info-item">
                                <span class="info-label">薪资标准：</span>
                                <span class="info-value">${formatValue(order.salary)}</span>
                            </div>
                            <div class="info-item">
                                <span class="info-label">上课时间：</span>
                                <span class="info-value">${formatValue(order.classTime)}</span>
                            </div>
                            <div class="info-item">
                                <span class="info-label">每周次数：</span>
                                <span class="info-value">${order.frequency > 0 ? order.frequency + '次' : '<span class="empty-value">暂无信息</span>'}</span>
                            </div>
                            <div class="info-item">
                                <span class="info-label">订单类型：</span>
                                <span class="info-value">${order.type === 'online' ? '线上订单' : order.type === 'fulltime' ? '全职订单' : '线下地区订单'}</span>
                            </div>
                        </div>

                        <!-- 学员情况卡片 -->
                        <div class="info-card">
                            <div class="info-card-title">学员情况</div>
                            <div class="info-item">
                                <span class="info-label">情况说明：</span>
                                <span class="info-value">${formatValue(order.studentSituation)}</span>
                            </div>
                        </div>

                        <!-- 教员要求卡片 -->
                        <div class="info-card">
                            <div class="info-card-title">教员要求</div>
                            <div class="info-item">
                                <span class="info-label">具体要求：</span>
                                <span class="info-value">${formatValue(order.teacherRequirement)}</span>
                            </div>
                        </div>
                    </div>
                </div>
                `;
            });

            orderList.innerHTML = html;
        }

        // 复制整单信息
        function copyOrder(orderId) {
            const order = allOrders.find(o => o.id === orderId);
            if (!order) return;

            const orderText = `${order.id}
【基础信息】
地区：${order.area || '暂无信息'}
详细地址：${order.address || '暂无信息'}
学员年级：${order.grade || '暂无信息'}
学员性别：${order.gender || '暂无信息'}
辅导科目：${order.subject || '暂无信息'}

【薪资与时间】
薪资标准：${order.salary || '暂无信息'}
上课时间：${order.classTime || '暂无信息'}
每周次数：${order.frequency > 0 ? order.frequency + '次' : '暂无信息'}
订单类型：${order.type === 'online' ? '线上订单' : order.type === 'fulltime' ? '全职订单' : '线下地区订单'}

【学员情况】
情况说明：${order.studentSituation || '暂无信息'}

【教员要求】
具体要求：${order.teacherRequirement || '暂无信息'}

【特殊标记】
${order.isDiscount ? '• 信息费折扣单' : ''}
${order.isHighSalary ? '• 高薪订单' : ''}
${order.isSpecial ? '• 特殊类订单' : ''}`.replace(/^\n+/, '').replace(/\n{3,}/g, '\n\n');

            navigator.clipboard.writeText(orderText).then(() => {
                alert('订单信息已复制到剪贴板！');
            }).catch(err => {
                alert('复制失败：' + err);
            });
        }

        // 复制地址
        function copyAddress(orderId) {
            const order = allOrders.find(o => o.id === orderId);
            if (!order) return;

            navigator.clipboard.writeText(order.address || '').then(() => {
                alert('地址已复制到剪贴板！');
            }).catch(err => {
                alert('复制失败：' + err);
            });
        }
    </script>
</body>
</html>
