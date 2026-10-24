<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sổ Tay Công Thức Toán 11 - Thầy Nguyễn Thanh Nhàn</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Google Fonts: Inter -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <!-- MathJax 3 Configuration & Library -->
    <script>
        window.MathJax = {
            tex: {
                inlineMath: [['$', '$'], ['\\(', '\\)']],
                displayMath: [['$$', '$$'], ['\\[', '\\]']],
                processEscapes: true
            },
            options: {
                ignoreHtmlClass: 'tex2jax_ignore',
                processHtmlClass: 'tex2jax_process'
            },
            startup: {
                pageReady: () => {
                    return MathJax.startup.defaultPageReady();
                }
            }
        };
    </script>
    <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>

    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                    },
                    colors: {
                        brand: {
                            50: '#f0f9ff',
                            100: '#e0f2fe',
                            500: '#0284c7',
                            600: '#0284c7',
                            700: '#0369a1',
                            800: '#075985',
                        }
                    }
                }
            }
        }
    </script>
    <style>
        body { font-family: 'Inter', sans-serif; }
        /* Custom scrollbar */
        ::-webkit-scrollbar { width: 6px; height: 6px; }
        ::-webkit-scrollbar-track { background: #f1f5f9; }
        ::-webkit-scrollbar-thumb { background: #cbd5e1; border-radius: 4px; }
        ::-webkit-scrollbar-thumb:hover { background: #94a3b8; }
        .mjx-chtml { font-size: 110% !important; }
    </style>
</head>
<body class="bg-slate-50 text-slate-800 min-h-screen flex flex-col antialiased selection:bg-sky-100 selection:text-sky-800">

    <!-- HEADER / NAVIGATION BAR -->
    <header class="bg-white border-b border-slate-200 sticky top-0 z-30 shadow-sm">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex items-center justify-between h-16">
                <!-- Logo & Title -->
                <div class="flex items-center space-x-3">
                    <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-sky-600 to-indigo-600 flex items-center justify-center text-white font-bold text-lg shadow-md shadow-sky-100">
                        <i class="fa-solid fa-square-root-variable"></i>
                    </div>
                    <div>
                        <h1 class="font-bold text-slate-900 text-base sm:text-lg leading-tight flex items-center gap-2">
                            Toán 11 <span class="hidden sm:inline-block text-xs px-2 py-0.5 bg-sky-100 text-sky-700 font-semibold rounded-full border border-sky-200">Thầy N.T.Nhàn</span>
                        </h1>
                        <p class="text-xs text-slate-500 hidden sm:block">THPT Ngô Gia Tự - Sổ tay & Ôn luyện công thức</p>
                    </div>
                </div>

                <!-- Mode & Active User Controls -->
                <div class="flex items-center space-x-3 sm:space-x-4">
                    <!-- Student Identity Selector -->
                    <div class="flex items-center bg-slate-100 p-1 rounded-xl border border-slate-200">
                        <span class="text-xs font-medium text-slate-500 px-2 hidden md:inline"><i class="fa-solid fa-user-graduate mr-1"></i>Học sinh:</span>
                        <select id="userSelect" onchange="changeActiveUser(this.value)" class="bg-white text-xs sm:text-sm font-semibold text-slate-700 py-1 px-2.5 rounded-lg border-0 focus:ring-2 focus:ring-sky-500 shadow-sm cursor-pointer outline-none">
                            <!-- Populated dynamically via JS -->
                        </select>
                    </div>

                    <!-- Role Switcher -->
                    <div class="bg-slate-100 p-1 rounded-xl flex items-center border border-slate-200">
                        <button id="btnStudentMode" onclick="switchRole('student')" class="px-3 py-1.5 rounded-lg text-xs sm:text-sm font-semibold transition-all duration-200 flex items-center gap-1.5 shadow-sm bg-white text-sky-700">
                            <i class="fa-solid fa-book-open"></i> <span class="hidden sm:inline">Học sinh</span>
                        </button>
                        <button id="btnTeacherMode" onclick="switchRole('teacher')" class="px-3 py-1.5 rounded-lg text-xs sm:text-sm font-semibold transition-all duration-200 text-slate-600 hover:text-slate-900 flex items-center gap-1.5">
                            <i class="fa-solid fa-chalkboard-user"></i> <span class="hidden sm:inline">Giáo viên</span>
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </header>

    <!-- MAIN CONTENT AREA -->
    <main class="flex-grow max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-6">

        <!-- ========================================== -->
        <!-- STUDENT MODE VIEW                          -->
        <!-- ========================================== -->
        <div id="studentView" class="space-y-6">
            <!-- Student Sub Navigation Tabs -->
            <div class="flex border-b border-slate-200 justify-between items-center bg-white px-4 pt-3 rounded-t-xl border border-b-0 shadow-sm">
                <div class="flex space-x-2 sm:space-x-6">
                    <button id="tabLearnBtn" onclick="switchStudentTab('learn')" class="pb-3 text-xs sm:text-sm font-bold border-b-2 border-sky-600 text-sky-600 flex items-center gap-2 transition-colors">
                        <i class="fa-solid fa-layer-group"></i> Tra cứu & Học thuộc
                    </button>
                    <button id="tabQuizBtn" onclick="switchStudentTab('quiz')" class="pb-3 text-xs sm:text-sm font-medium border-b-2 border-transparent text-slate-500 hover:text-slate-700 flex items-center gap-2 transition-colors">
                        <i class="fa-solid fa-circle-question"></i> Kiểm tra Luyện tập
                    </button>
                </div>
                <!-- Global Progress Badge -->
                <div class="pb-3 hidden sm:flex items-center gap-2">
                    <span class="text-xs font-semibold text-slate-500">Tiến độ chung:</span>
                    <div class="w-32 bg-slate-100 rounded-full h-2.5 border border-slate-200 overflow-hidden">
                        <div id="globalProgressBar" class="bg-gradient-to-r from-sky-500 to-emerald-500 h-2.5 rounded-full transition-all duration-300" style="width: 0%"></div>
                    </div>
                    <span id="globalProgressText" class="text-xs font-bold text-slate-700">0%</span>
                </div>
            </div>

            <!-- TAB 1: LEARN & FLASHCARDS -->
            <div id="studentTabLearn" class="grid grid-cols-1 lg:grid-cols-4 gap-6">
                <!-- Sidebar Category Selector -->
                <div class="lg:col-span-1 space-y-4">
                    <div class="bg-white p-4 rounded-xl border border-slate-200 shadow-sm">
                        <h3 class="text-xs font-bold text-slate-400 uppercase tracking-wider mb-3 flex items-center justify-between">
                            <span>Chủ đề kiến thức</span>
                            <i class="fa-solid fa-bookmark text-sky-500"></i>
                        </h3>
                        <nav class="space-y-1.5" id="categoryList">
                            <!-- Populated dynamically -->
                        </nav>
                    </div>

                    <!-- Filter Box -->
                    <div class="bg-white p-4 rounded-xl border border-slate-200 shadow-sm space-y-3">
                        <h4 class="text-xs font-bold text-slate-400 uppercase tracking-wider">Lọc & Tìm kiếm</h4>
                        <div class="relative">
                            <i class="fa-solid fa-magnifying-glass absolute left-3 top-2.5 text-slate-400 text-xs"></i>
                            <input type="text" id="searchInput" oninput="renderFormulaList()" placeholder="Tìm tên công thức..." class="w-full pl-8 pr-3 py-1.5 text-xs rounded-lg border border-slate-200 focus:outline-none focus:ring-2 focus:ring-sky-500">
                        </div>
                        <div class="flex gap-1 bg-slate-100 p-1 rounded-lg">
                            <button onclick="setFilter('all')" id="filterAll" class="flex-1 py-1 text-xs font-semibold rounded text-center bg-white text-slate-800 shadow-sm">Tất cả</button>
                            <button onclick="setFilter('unlearned')" id="filterUnlearned" class="flex-1 py-1 text-xs font-semibold rounded text-center text-slate-600 hover:text-slate-900">Chưa thuộc</button>
                            <button onclick="setFilter('learned')" id="filterLearned" class="flex-1 py-1 text-xs font-semibold rounded text-center text-slate-600 hover:text-slate-900">Đã thuộc</button>
                        </div>
                    </div>
                </div>

                <!-- Main Formulas Cards Display Area -->
                <div class="lg:col-span-3 space-y-4">
                    <!-- Category Header Info -->
                    <div id="categoryHeaderCard" class="bg-white p-5 rounded-xl border border-slate-200 shadow-sm flex flex-col sm:flex-row justify-between items-start sm:items-center gap-3">
                        <div>
                            <h2 id="currentCategoryTitle" class="text-lg font-bold text-slate-900">Đang tải...</h2>
                            <p id="currentCategoryDesc" class="text-xs text-slate-500 mt-0.5">Tóm tắt kiến thức cốt lõi</p>
                        </div>
                        <div class="flex items-center gap-3 w-full sm:w-auto justify-between sm:justify-end">
                            <div class="text-right">
                                <span class="text-xs text-slate-500">Đã thuộc:</span>
                                <span id="categoryProgressText" class="text-sm font-bold text-emerald-600 ml-1">0/0</span>
                            </div>
                            <button onclick="markAllInCategoryLearned()" class="px-3 py-1.5 bg-emerald-50 text-emerald-700 hover:bg-emerald-100 border border-emerald-200 rounded-lg text-xs font-semibold transition flex items-center gap-1.5">
                                <i class="fa-solid fa-check-double"></i> Thuộc tất cả
                            </button>
                        </div>
                    </div>

                    <!-- Grid of Formulas -->
                    <div id="formulaGrid" class="grid grid-cols-1 md:grid-cols-2 gap-4">
                        <!-- Cards dynamically rendered here -->
                    </div>
                </div>
            </div>

            <!-- TAB 2: QUIZ TESTING MODE -->
            <div id="studentTabQuiz" class="hidden max-w-3xl mx-auto space-y-6">
                <!-- Start Quiz Intro Card -->
                <div id="quizIntroCard" class="bg-white p-8 rounded-2xl border border-slate-200 shadow-sm text-center space-y-5">
                    <div class="w-16 h-16 bg-sky-100 text-sky-600 rounded-2xl flex items-center justify-center mx-auto text-2xl font-bold shadow-inner">
                        <i class="fa-solid fa-vial-circle-check"></i>
                    </div>
                    <div class="space-y-2">
                        <h2 class="text-2xl font-bold text-slate-900">Kiểm Tra Luyện Tập Công Thức</h2>
                        <p class="text-sm text-slate-600 max-w-md mx-auto">Bài kiểm tra gồm 10 câu hỏi trắc nghiệm được lấy ngẫu nhiên từ ngân hàng câu hỏi Toán 11. Hệ thống sẽ ghi nhận điểm số vào hồ sơ của bạn.</p>
                    </div>
                    <div class="pt-2">
                        <button onclick="startQuiz()" class="px-6 py-3 bg-gradient-to-r from-sky-600 to-indigo-600 text-white font-bold rounded-xl shadow-lg shadow-sky-200 hover:shadow-xl hover:scale-105 transition-all duration-200 flex items-center gap-2 mx-auto">
                            <i class="fa-solid fa-play"></i> Bắt đầu làm bài ngay (10 câu)
                        </button>
                    </div>
                </div>

                <!-- Active Quiz Card -->
                <div id="quizActiveCard" class="hidden bg-white p-6 rounded-2xl border border-slate-200 shadow-md space-y-6">
                    <!-- Top Progress Info -->
                    <div class="flex items-center justify-between border-b border-slate-100 pb-4">
                        <div class="flex items-center space-x-2">
                            <span class="text-xs font-bold text-sky-600 bg-sky-50 border border-sky-200 px-3 py-1 rounded-full">
                                Câu hỏi <span id="quizCurrentNum">1</span>/10
                            </span>
                            <span id="quizCategoryBadge" class="text-xs font-semibold text-slate-500 bg-slate-100 px-2.5 py-1 rounded-full">
                                Lượng giác
                            </span>
                        </div>
                        <div class="text-xs font-semibold text-slate-500">
                            Điểm hiện tại: <span id="quizCurrentScore" class="text-emerald-600 font-bold">0</span>
                        </div>
                    </div>

                    <!-- Question Content -->
                    <div class="space-y-3">
                        <h3 id="quizQuestionText" class="text-base sm:text-lg font-semibold text-slate-800 leading-relaxed">
                            Loading question...
                        </h3>
                    </div>

                    <!-- Answer Options -->
                    <div id="quizOptionsContainer" class="grid grid-cols-1 gap-3">
                        <!-- Options populated dynamically -->
                    </div>

                    <!-- Instant Explanation Panel -->
                    <div id="quizExplanationPanel" class="hidden p-4 rounded-xl border bg-slate-50 text-xs sm:text-sm space-y-1 transition-all">
                        <div class="font-bold flex items-center gap-1.5" id="quizResultBadge">
                            <!-- Correct / Incorrect status -->
                        </div>
                        <div id="quizExplanationText" class="text-slate-700 leading-relaxed pt-1">
                            <!-- Explanation latex -->
                        </div>
                    </div>

                    <!-- Footer Action -->
                    <div class="flex justify-end pt-2 border-t border-slate-100">
                        <button id="btnNextQuestion" onclick="nextQuestion()" disabled class="px-5 py-2.5 bg-slate-200 text-slate-400 font-bold rounded-xl text-xs sm:text-sm cursor-not-allowed transition flex items-center gap-2">
                            Câu tiếp theo <i class="fa-solid fa-arrow-right"></i>
                        </button>
                    </div>
                </div>

                <!-- Quiz Results Card -->
                <div id="quizResultCard" class="hidden bg-white p-8 rounded-2xl border border-slate-200 shadow-md text-center space-y-6">
                    <div id="quizResultIcon" class="w-20 h-20 rounded-full flex items-center justify-center mx-auto text-3xl font-bold">
                        <!-- Dynamic Icon -->
                    </div>
                    <div class="space-y-2">
                        <h2 class="text-2xl font-bold text-slate-900">Hoàn Thành Bài Kiểm Tra!</h2>
                        <p class="text-sm text-slate-500">Kết quả của bạn đã được cập nhật tự động vào hệ thống.</p>
                    </div>

                    <!-- Score Badge Box -->
                    <div class="bg-slate-50 p-6 rounded-2xl border border-slate-200 max-w-xs mx-auto space-y-2">
                        <div class="text-xs font-bold uppercase tracking-wider text-slate-400">Tổng điểm số</div>
                        <div class="text-4xl font-extrabold text-slate-800" id="quizFinalScore">0/10</div>
                        <div id="quizGradeBadge" class="inline-block text-xs font-bold px-3 py-1 rounded-full mt-1">
                            Xuất sắc
                        </div>
                    </div>

                    <p id="quizAdviceText" class="text-sm text-slate-600 max-w-md mx-auto italic">
                        "Hãy tiếp tục duy trì phong độ và ôn tập đều đặn các công thức chưa thuộc!"
                    </p>

                    <div class="flex justify-center gap-3 pt-2">
                        <button onclick="startQuiz()" class="px-5 py-2.5 bg-sky-600 text-white font-bold rounded-xl hover:bg-sky-700 transition text-sm flex items-center gap-2">
                            <i class="fa-solid fa-rotate-right"></i> Làm bài thi khác
                        </button>
                        <button onclick="switchStudentTab('learn')" class="px-5 py-2.5 bg-slate-100 text-slate-700 hover:bg-slate-200 font-bold rounded-xl transition text-sm flex items-center gap-2">
                            <i class="fa-solid fa-book-open"></i> Xem lại công thức
                        </button>
                    </div>
                </div>
            </div>
        </div>

        <!-- ========================================== -->
        <!-- TEACHER MODE VIEW                          -->
        <!-- ========================================== -->
        <div id="teacherView" class="hidden space-y-6">
            <!-- Dashboard Title Bar -->
            <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-4 bg-white p-5 rounded-2xl border border-slate-200 shadow-sm">
                <div>
                    <h2 class="text-xl font-bold text-slate-900 flex items-center gap-2">
                        <i class="fa-solid fa-chart-pie text-sky-600"></i> Bảng Theo Dõi Tiến Độ Lớp Học
                    </h2>
                    <p class="text-xs text-slate-500 mt-1">Quản lý kết quả học thuộc công thức & điểm số thi thử của học sinh</p>
                </div>
                <div class="flex items-center gap-2">
                    <button onclick="showAddStudentModal()" class="px-3.5 py-2 bg-sky-600 hover:bg-sky-700 text-white rounded-xl text-xs font-bold shadow-sm transition flex items-center gap-1.5">
                        <i class="fa-solid fa-user-plus"></i> Thêm học sinh
                    </button>
                    <button onclick="confirmResetAllData()" class="px-3.5 py-2 bg-rose-50 text-rose-600 hover:bg-rose-100 border border-rose-200 rounded-xl text-xs font-bold transition flex items-center gap-1.5">
                        <i class="fa-solid fa-rotate-left"></i> Đặt lại dữ liệu mẫu
                    </button>
                </div>
            </div>

            <!-- Analytics Overview Cards -->
            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
                <!-- Card 1 -->
                <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-sm flex items-center justify-between">
                    <div>
                        <p class="text-xs font-semibold text-slate-400 uppercase tracking-wider">Sĩ số lớp</p>
                        <h4 id="statTotalStudents" class="text-2xl font-extrabold text-slate-800 mt-1">0</h4>
                        <span class="text-[11px] text-slate-500">Học sinh trong danh sách</span>
                    </div>
                    <div class="w-12 h-12 bg-sky-50 text-sky-600 rounded-xl flex items-center justify-center text-xl">
                        <i class="fa-solid fa-users"></i>
                    </div>
                </div>

                <!-- Card 2 -->
                <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-sm flex items-center justify-between">
                    <div>
                        <p class="text-xs font-semibold text-slate-400 uppercase tracking-wider">Công thức hoàn thành</p>
                        <h4 id="statTotalLearned" class="text-2xl font-extrabold text-emerald-600 mt-1">0</h4>
                        <span class="text-[11px] text-slate-500">Lượt bấm "Đã thuộc"</span>
                    </div>
                    <div class="w-12 h-12 bg-emerald-50 text-emerald-600 rounded-xl flex items-center justify-center text-xl">
                        <i class="fa-solid fa-circle-check"></i>
                    </div>
                </div>

                <!-- Card 3 -->
                <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-sm flex items-center justify-between">
                    <div>
                        <p class="text-xs font-semibold text-slate-400 uppercase tracking-wider">Điểm TB Lớp</p>
                        <h4 id="statAverageScore" class="text-2xl font-extrabold text-indigo-600 mt-1">0.0</h4>
                        <span class="text-[11px] text-slate-500">Thang điểm 10</span>
                    </div>
                    <div class="w-12 h-12 bg-indigo-50 text-indigo-600 rounded-xl flex items-center justify-center text-xl">
                        <i class="fa-solid fa-graduation-cap"></i>
                    </div>
                </div>

                <!-- Card 4 -->
                <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-sm flex items-center justify-between">
                    <div>
                        <p class="text-xs font-semibold text-slate-400 uppercase tracking-wider">Tỷ lệ đạt (>=5.0)</p>
                        <h4 id="statPassRate" class="text-2xl font-extrabold text-amber-600 mt-1">0%</h4>
                        <span class="text-[11px] text-slate-500">Đạt yêu cầu bài thi</span>
                    </div>
                    <div class="w-12 h-12 bg-amber-50 text-amber-600 rounded-xl flex items-center justify-center text-xl">
                        <i class="fa-solid fa-award"></i>
                    </div>
                </div>
            </div>

            <!-- Student Detail List Table -->
            <div class="bg-white rounded-2xl border border-slate-200 shadow-sm overflow-hidden">
                <div class="p-4 border-b border-slate-100 flex justify-between items-center bg-slate-50/50">
                    <h3 class="font-bold text-slate-800 text-sm flex items-center gap-2">
                        <i class="fa-solid fa-list-check text-sky-600"></i> Danh Sách Tiến Độ Chi Tiết
                    </h3>
                    <span class="text-xs text-slate-500">Cập nhật thời gian thực</span>
                </div>
                <div class="overflow-x-auto">
                    <table class="w-full text-left border-collapse">
                        <thead>
                            <tr class="border-b border-slate-200 bg-slate-50 text-[11px] font-bold text-slate-500 uppercase tracking-wider">
                                <th class="py-3 px-4">Họ và Tên</th>
                                <th class="py-3 px-4">Số công thức đã thuộc</th>
                                <th class="py-3 px-4 text-center">Số lần làm bài</th>
                                <th class="py-3 px-4 text-center">Điểm trung bình</th>
                                <th class="py-3 px-4">Đánh giá tiến độ</th>
                                <th class="py-3 px-4 text-right">Thao tác</th>
                            </tr>
                        </thead>
                        <tbody id="teacherStudentTable" class="divide-y divide-slate-100 text-xs sm:text-sm">
                            <!-- Populated dynamically -->
                        </tbody>
                    </table>
                </div>
            </div>
        </div>

    </main>

    <!-- FOOTER -->
    <footer class="bg-white border-t border-slate-200 py-4 mt-auto">
        <div class="max-w-7xl mx-auto px-4 text-center text-xs text-slate-500 space-y-1">
            <p class="font-medium text-slate-700">Ứng dụng Ôn tập & Kiểm tra Công thức Toán 11 - THPT Ngô Gia Tự</p>
            <p>Biên soạn nội dung: <span class="font-semibold text-slate-800">Thầy Nguyễn Thanh Nhàn</span> | Phát triển hệ thống UI/UX Web App</p>
        </div>
    </footer>

    <!-- MODAL: ADD STUDENT -->
    <div id="addStudentModal" class="fixed inset-0 bg-slate-900/40 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
        <div class="bg-white rounded-2xl max-w-md w-full p-6 space-y-4 shadow-xl border border-slate-100">
            <div class="flex justify-between items-center border-b border-slate-100 pb-3">
                <h3 class="font-bold text-slate-900 text-base">Thêm Học Sinh Mới</h3>
                <button onclick="closeAddStudentModal()" class="text-slate-400 hover:text-slate-600"><i class="fa-solid fa-xmark text-lg"></i></button>
            </div>
            <div>
                <label class="block text-xs font-semibold text-slate-700 mb-1">Họ và Tên Học Sinh:</label>
                <input type="text" id="newStudentName" placeholder="Nhập họ tên (Ví dụ: Nguyễn Văn A)" class="w-full px-3 py-2 text-sm border border-slate-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-sky-500">
            </div>
            <div class="flex justify-end gap-2 pt-2">
                <button onclick="closeAddStudentModal()" class="px-4 py-2 bg-slate-100 text-slate-600 font-bold rounded-xl text-xs hover:bg-slate-200">Hủy</button>
                <button onclick="saveNewStudent()" class="px-4 py-2 bg-sky-600 text-white font-bold rounded-xl text-xs hover:bg-sky-700">Thêm học sinh</button>
            </div>
        </div>
    </div>

    <!-- MODAL: CONFIRM ACTION -->
    <div id="confirmModal" class="fixed inset-0 bg-slate-900/40 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
        <div class="bg-white rounded-2xl max-w-sm w-full p-6 space-y-4 shadow-xl text-center">
            <div class="w-12 h-12 bg-rose-100 text-rose-600 rounded-full flex items-center justify-center mx-auto text-xl">
                <i class="fa-solid fa-triangle-exclamation"></i>
            </div>
            <h3 id="confirmTitle" class="font-bold text-slate-900 text-base">Xác nhận thao tác</h3>
            <p id="confirmMessage" class="text-xs text-slate-500">Bạn có chắc chắn muốn thực hiện hành động này?</p>
            <div class="flex justify-center gap-2 pt-2">
                <button onclick="closeConfirmModal()" class="px-4 py-2 bg-slate-100 text-slate-600 font-bold rounded-xl text-xs hover:bg-slate-200">Hủy bỏ</button>
                <button id="btnConfirmAction" class="px-4 py-2 bg-rose-600 text-white font-bold rounded-xl text-xs hover:bg-rose-700">Xác nhận</button>
            </div>
        </div>
    </div>


    <!-- JAVASCRIPT APP LOGIC -->
    <script>
        /* ==========================================================================
           1. FORMULAS & QUIZ KNOWLEDGE BANK (NGUYEN THANH NHAN - TOAN 11)
           ========================================================================== */
        const FORMULA_DATABASE = [
            // CATEGORY 1: LƯỢNG GIÁC
            {
                id: 'lg_1',
                categoryId: 'cat_lg',
                categoryName: 'Lượng giác',
                title: 'Hệ thức lượng giác cơ bản',
                latex: '\\sin^2 x + \\cos^2 x = 1, \\quad 1 + \\tan^2 x = \\frac{1}{\\cos^2 x} \\quad (x \\neq \\frac{\\pi}{2} + k\\pi)',
                note: 'Điều kiện: $\\cos x \\neq 0$ cho $\\tan x$ và $\\sin x \\neq 0$ cho $\\cot x$.'
            },
            {
                id: 'lg_2',
                categoryId: 'cat_lg',
                categoryName: 'Lượng giác',
                title: 'Công thức cộng lượng giác',
                latex: '\\sin(a \\pm b) = \\sin a \\cos b \\pm \\cos a \\sin b \\\\ \\cos(a \\pm b) = \\cos a \\cos b \\mp \\sin a \\sin b',
                note: 'Mẹo nhớ: Sin thì sin cos cos sin; Cos thì cos cos sin sin coi chừng đổi dấu.'
            },
            {
                id: 'lg_3',
                categoryId: 'cat_lg',
                categoryName: 'Lượng giác',
                title: 'Công thức nhân đôi',
                latex: '\\sin 2x = 2\\sin x \\cos x \\\\ \\cos 2x = \\cos^2 x - \\sin^2 x = 2\\cos^2 x - 1 = 1 - 2\\sin^2 x',
                note: 'Công thức hạ bậc tương ứng: $\\cos^2 x = \\frac{1+\\cos 2x}{2}$, $\\sin^2 x = \\frac{1-\\cos 2x}{2}$.'
            },
            {
                id: 'lg_4',
                categoryId: 'cat_lg',
                categoryName: 'Lượng giác',
                title: 'Phương trình lượng giác cơ bản',
                latex: '\\sin x = \\sin \\alpha \\Leftrightarrow \\begin{bmatrix} x = \\alpha + k2\\pi \\\\ x = \\pi - \\alpha + k2\\pi \\end{bmatrix} (k \\in \\mathbb{Z})',
                note: 'Đối với $\\cos x = \\cos \\alpha \\Leftrightarrow x = \\pm \\alpha + k2\\pi$.'
            },

            // CATEGORY 2: ĐẠI SỐ TỔ HỢP
            {
                id: 'th_1',
                categoryId: 'cat_th',
                categoryName: 'Đại số tổ hợp',
                title: 'Hoán vị, Chỉnh hợp & Tổ hợp',
                latex: 'P_n = n!, \\quad A_n^k = \\frac{n!}{(n-k)!}, \\quad C_n^k = \\frac{n!}{k!(n-k)!} \\quad (0 \\le k \\le n)',
                note: 'Chỉnh hợp $A_n^k$ có phân biệt thứ tự, Tổ hợp $C_n^k$ không phân biệt thứ tự.'
            },
            {
                id: 'th_2',
                categoryId: 'cat_th',
                categoryName: 'Đại số tổ hợp',
                title: 'Tính chất của Tổ hợp',
                latex: 'C_n^k = C_n^{n-k}, \\quad C_n^k + C_n^{k+1} = C_{n+1}^{k+1}',
                note: 'Ứng dụng trong tam giác Pascal.'
            },
            {
                id: 'th_3',
                categoryId: 'cat_th',
                categoryName: 'Đại số tổ hợp',
                title: 'Khai triển Nhị thức Newton',
                latex: '(a+b)^n = \\sum_{k=0}^{n} C_n^k a^{n-k} b^k = C_n^0 a^n + C_n^1 a^{n-1}b + \\dots + C_n^n b^n',
                note: 'Số hạng tổng quát thứ $(k+1)$ là $T_{k+1} = C_n^k a^{n-k} b^k$.'
            },

            // CATEGORY 3: DÃY SỐ - CẤP SỐ CỘNG & CẤP SỐ NHÂN
            {
                id: 'ds_1',
                categoryId: 'cat_ds',
                categoryName: 'Dãy số & Cấp số',
                title: 'Cấp số cộng (CSC)',
                latex: 'u_n = u_1 + (n-1)d, \\quad S_n = \\frac{n(u_1 + u_n)}{2} = \\frac{n[2u_1 + (n-1)d]}{2}',
                note: 'Tính chất ba số hạng liên tiếp: $u_k = \\frac{u_{k-1} + u_{k+1}}{2}$.'
            },
            {
                id: 'ds_2',
                categoryId: 'cat_ds',
                categoryName: 'Dãy số & Cấp số',
                title: 'Cấp số nhân (CSN)',
                latex: 'u_n = u_1 \\cdot q^{n-1}, \\quad S_n = u_1 \\frac{1 - q^n}{1 - q} \\quad (q \\neq 1)',
                note: 'Tính chất ba số hạng liên tiếp: $u_k^2 = u_{k-1} \\cdot u_{k+1}$.'
            },

            // CATEGORY 4: GIỚI HẠN & ĐẠO HÀM
            {
                id: 'dh_1',
                categoryId: 'cat_dh',
                categoryName: 'Giới hạn & Đạo hàm',
                title: 'Bảng đạo hàm sơ cấp cơ bản',
                latex: '(x^n)\' = n x^{n-1}, \\quad (\\sqrt{x})\' = \\frac{1}{2\\sqrt{x}}, \\quad (\\sin x)\' = \\cos x, \\quad (\\cos x)\' = -\\sin x',
                note: 'Đạo hàm của hằng số $(c)\' = 0$.'
            },
            {
                id: 'dh_2',
                categoryId: 'cat_dh',
                categoryName: 'Giới hạn & Đạo hàm',
                title: 'Quy tắc tính đạo hàm (Tổng, Tích, Thương)',
                latex: '(u \\pm v)\' = u\' \\pm v\', \\quad (u \\cdot v)\' = u\'v + uv\', \\quad \\left(\\frac{u}{v}\\right)\' = \\frac{u\'v - uv\'}{v^2}',
                note: 'Trường hợp đặc biệt: $\\left(\\frac{1}{v}\\right)\' = -\\frac{v\'}{v^2}$.'
            },
            {
                id: 'dh_3',
                categoryId: 'cat_dh',
                categoryName: 'Giới hạn & Đạo hàm',
                title: 'Phương trình tiếp tuyến của đồ thị hàm số',
                latex: 'y = f\'(x_0)(x - x_0) + y_0',
                note: 'Trong đó $x_0$ là hoành độ tiếp điểm, $k = f\'(x_0)$ là hệ số góc tiếp tuyến.'
            },

            // CATEGORY 5: HÌNH HỌC & HỆ THỨC LƯỢNG
            {
                id: 'hh_1',
                categoryId: 'cat_hh',
                categoryName: 'Hình học & Tam giác',
                title: 'Định lý Cosin trong tam giác',
                latex: 'a^2 = b^2 + c^2 - 2bc \\cos A, \\quad \\cos A = \\frac{b^2 + c^2 - a^2}{2bc}',
                note: 'Áp dụng tính cạnh thứ 3 khi biết 2 cạnh và góc kẹp giữa.'
            },
            {
                id: 'hh_2',
                categoryId: 'cat_hh',
                categoryName: 'Hình học & Tam giác',
                title: 'Định lý Sin trong tam giác',
                latex: '\\frac{a}{\\sin A} = \\frac{b}{\\sin B} = \\frac{c}{\\sin C} = 2R',
                note: 'R là bán kính đường tròn ngoại tiếp tam giác ABC.'
            },
            {
                id: 'hh_3',
                categoryId: 'cat_hh',
                categoryName: 'Hình học & Tam giác',
                title: 'Các công thức tính diện tích tam giác',
                latex: 'S = \\frac{1}{2}a h_a = \\frac{1}{2}bc \\sin A = \\frac{abc}{4R} = p r = \\sqrt{p(p-a)(p-b)(p-c)}',
                note: 'Trong đó $p = \\frac{a+b+c}{2}$ là nửa chu vi, $r$ là bán kính đường tròn nội tiếp.'
            }
        ];

        const CATEGORIES = [
            { id: 'cat_lg', name: '1. Lượng giác', icon: 'fa-wave-square', desc: 'Hệ thức cơ bản, công thức cộng, nhân đôi & phương trình LG' },
            { id: 'cat_th', name: '2. Đại số tổ hợp', icon: 'fa-arrow-up-1-9', desc: 'Hoán vị, Chỉnh hợp, Tổ hợp & Nhị thức Newton' },
            { id: 'cat_ds', name: '3. Dãy số - CSC & CSN', icon: 'fa-arrow-trend-up', desc: 'Công thức số hạng tổng quát & tổng n số hạng' },
            { id: 'cat_dh', name: '4. Giới hạn & Đạo hàm', icon: 'fa-calculator', desc: 'Bảng đạo hàm sơ cấp, quy tắc tính & tiếp tuyến' },
            { id: 'cat_hh', name: '5. Hình học & Tam giác', icon: 'fa-shapes', desc: 'Định lý Sin, Cosin & Công thức diện tích' }
        ];

        // QUIZ QUESTION BANK
        const QUIZ_BANK = [
            {
                category: 'Lượng giác',
                question: 'Công thức nào sau đây là ĐÚNG đối với công thức cộng của $\\cos(a + b)$?',
                options: [
                    '$\\cos(a + b) = \\cos a \\cos b - \\sin a \\sin b$',
                    '$\\cos(a + b) = \\cos a \\cos b + \\sin a \\sin b$',
                    '$\\cos(a + b) = \\sin a \\cos b + \\cos a \\sin b$',
                    '$\\cos(a + b) = \\sin a \\cos b - \\cos a \\sin b$'
                ],
                correct: 0,
                explanation: 'Theo công thức cộng lượng giác: $\\cos(a + b) = \\cos a \\cos b - \\sin a \\sin b$.'
            },
            {
                category: 'Lượng giác',
                question: 'Khẳng định nào sau đây là ĐÚNG với mọi $x$ làm cho các biểu thức có nghĩa?',
                options: [
                    '$\\sin 2x = 2\\sin x \\cos x$',
                    '$\\sin 2x = \\sin x \\cos x$',
                    '$\\cos 2x = \\cos^2 x + \\sin^2 x$',
                    '\\tan 2x = 2\\tan x'
                ],
                correct: 0,
                explanation: 'Công thức nhân đôi: $\\sin 2x = 2\\sin x \\cos x$.'
            },
            {
                category: 'Đại số tổ hợp',
                question: 'Công thức tính số tổ hợp chập $k$ của $n$ phần tử ($0 \\le k \\le n$) là:',
                options: [
                    '$C_n^k = \\frac{n!}{k!(n-k)!}$',
                    '$C_n^k = \\frac{n!}{(n-k)!}$',
                    '$C_n^k = \\frac{n!}{k!}$',
                    '$C_n^k = n! \\cdot k!$'
                ],
                correct: 0,
                explanation: 'Tổ hợp không phân biệt thứ tự: $C_n^k = \\frac{n!}{k!(n-k)!}$.'
            },
            {
                category: 'Đại số tổ hợp',
                question: 'Số hạng tổng quát thứ $(k+1)$ trong khai triển nhị thức Newton $(a+b)^n$ là:',
                options: [
                    '$T_{k+1} = C_n^k a^{n-k} b^k$',
                    '$T_{k+1} = C_n^k a^k b^{n-k}$',
                    '$T_{k+1} = A_n^k a^{n-k} b^k$',
                    '$T_{k+1} = C_n^{k+1} a^{n-k} b^k$'
                ],
                correct: 0,
                explanation: 'Số hạng thứ $k+1$ trong khai triển nhị thức Newton chuẩn là $T_{k+1} = C_n^k a^{n-k} b^k$.'
            },
            {
                category: 'Dãy số & Cấp số',
                question: 'Cho Cấp số cộng có số hạng đầu $u_1$ và công sai $d$. Số hạng tổng quát $u_n$ ($n \\ge 2$) được tính bằng:',
                options: [
                    '$u_n = u_1 + (n-1)d$',
                    '$u_n = u_1 + n d$',
                    '$u_n = u_1 \\cdot d^{n-1}$',
                    '$u_n = u_1 + (n+1)d$'
                ],
                correct: 0,
                explanation: 'Số hạng tổng quát Cấp số cộng: $u_n = u_1 + (n-1)d$.'
            },
            {
                category: 'Dãy số & Cấp số',
                question: 'Cho Cấp số nhân có số hạng đầu $u_1$ và công bội $q \\neq 1$. Tổng $n$ số hạng đầu $S_n$ là:',
                options: [
                    '$S_n = u_1 \\frac{1 - q^n}{1 - q}$',
                    '$S_n = u_1 \\frac{1 - q}{1 - q^n}$',
                    '$S_n = \\frac{u_1(1 - q)}{q^n}$',
                    '$S_n = u_1 \\cdot q^{n-1}$'
                ],
                correct: 0,
                explanation: 'Công thức tính tổng $n$ số hạng đầu của Cấp số nhân: $S_n = u_1 \\frac{1 - q^n}{1 - q}$.'
            },
            {
                category: 'Giới hạn & Đạo hàm',
                question: 'Đạo hàm của hàm số $y = \\sqrt{x}$ (với $x > 0$) là:',
                options: [
                    '$y\' = \\frac{1}{2\\sqrt{x}}$',
                    '$y\' = \\frac{1}{\\sqrt{x}}$',
                    '$y\' = 2\\sqrt{x}$',
                    '$y\' = -\\frac{1}{2\\sqrt{x}}$'
                ],
                correct: 0,
                explanation: 'Theo bảng đạo hàm hàm số sơ cấp: $(\\sqrt{x})\' = \\frac{1}{2\\sqrt{x}}$.'
            },
            {
                category: 'Giới hạn & Đạo hàm',
                question: 'Đạo hàm của tích hai hàm số $(u \\cdot v)\'$ bằng:',
                options: [
                    '$(u \\cdot v)\' = u\'v + uv\'$',
                    '$(u \\cdot v)\' = u\'v - uv\'$',
                    '$(u \\cdot v)\' = u\' \\cdot v\'$',
                    '$(u \\cdot v)\' = u\'v + v\'$'
                ],
                correct: 0,
                explanation: 'Quy tắc tính đạo hàm của một tích: $(u \\cdot v)\' = u\'v + uv\'$.'
            },
            {
                category: 'Hình học & Tam giác',
                question: 'Trong tam giác $ABC$, định lý Cosin để tính cạnh $a^2$ là:',
                options: [
                    '$a^2 = b^2 + c^2 - 2bc \\cos A$',
                    '$a^2 = b^2 + c^2 + 2bc \\cos A$',
                    '$a^2 = b^2 + c^2 - bc \\cos A$',
                    '$a^2 = b^2 - c^2 - 2bc \\cos A$'
                ],
                correct: 0,
                explanation: 'Theo định lý Cosin trong tam giác: $a^2 = b^2 + c^2 - 2bc \\cos A$.'
            },
            {
                category: 'Hình học & Tam giác',
                question: 'Công thức Heron tính diện tích tam giác $ABC$ với $p = \\frac{a+b+c}{2}$ là:',
                options: [
                    '$S = \\sqrt{p(p-a)(p-b)(p-c)}$',
                    '$S = p(p-a)(p-b)(p-c)$',
                    '$S = \\sqrt{(p-a)(p-b)(p-c)}$',
                    '$S = \\frac{1}{2}\\sqrt{p(p-a)(p-b)(p-c)}$'
                ],
                correct: 0,
                explanation: 'Công thức Heron: $S = \\sqrt{p(p-a)(p-b)(p-c)}$.'
            }
        ];

        /* ==========================================================================
           2. MOCK INITIAL DATA & LOCALSTORAGE STATE MANAGEMENT
           ========================================================================== */
        const INITIAL_STUDENTS = [
            {
                id: 'stu_1',
                name: 'Nguyễn Văn An',
                learnedFormulas: ['lg_1', 'lg_2', 'th_1', 'ds_1', 'dh_1', 'hh_1'],
                quizHistory: [
                    { date: '2026-10-20', score: 8, total: 10 },
                    { date: '2026-10-22', score: 9, total: 10 }
                ]
            },
            {
                id: 'stu_2',
                name: 'Trần Thị Bích',
                learnedFormulas: ['lg_1', 'lg_3', 'th_1', 'th_2', 'th_3', 'ds_1', 'ds_2', 'dh_1', 'dh_2', 'hh_1', 'hh_2'],
                quizHistory: [
                    { date: '2026-10-21', score: 10, total: 10 }
                ]
            },
            {
                id: 'stu_3',
                name: 'Lê Hoàng Cường',
                learnedFormulas: ['lg_1', 'ds_1'],
                quizHistory: [
                    { date: '2026-10-18', score: 4, total: 10 }
                ]
            },
            {
                id: 'stu_4',
                name: 'Phạm Minh Đức',
                learnedFormulas: ['lg_1', 'lg_2', 'lg_3', 'th_1', 'dh_1'],
                quizHistory: [
                    { date: '2026-10-23', score: 6, total: 10 }
                ]
            }
        ];

        // Global State Variables
        let appData = {
            activeRole: 'student', // 'student' | 'teacher'
            activeStudentId: 'stu_1',
            activeCategory: 'cat_lg',
            filterStatus: 'all', // 'all' | 'unlearned' | 'learned'
            students: []
        };

        // Quiz State Variables
        let currentQuiz = {
            questions: [],
            currentIndex: 0,
            score: 0,
            selectedOption: null,
            isAnswered: false
        };

        /* ==========================================================================
           3. INITIALIZATION & STORAGE HELPER FUNCTIONS
           ========================================================================== */
        window.onload = function() {
            loadDataFromStorage();
            initUI();
            renderAll();
        };

        function loadDataFromStorage() {
            const stored = localStorage.getItem('toan11_app_data');
            if (stored) {
                try {
                    const parsed = JSON.parse(stored);
                    appData.students = parsed.students || INITIAL_STUDENTS;
                    appData.activeStudentId = parsed.activeStudentId || 'stu_1';
                } catch(e) {
                    appData.students = INITIAL_STUDENTS;
                }
            } else {
                appData.students = JSON.parse(JSON.stringify(INITIAL_STUDENTS));
                saveDataToStorage();
            }
        }

        function saveDataToStorage() {
            localStorage.setItem('toan11_app_data', JSON.stringify({
                students: appData.students,
                activeStudentId: appData.activeStudentId
            }));
        }

        function triggerMathJax() {
            if (window.MathJax && window.MathJax.typesetPromise) {
                window.MathJax.typesetPromise().catch((err) => console.log('MathJax error:', err));
            }
        }

        /* ==========================================================================
           4. CORE UI RENDERING & EVENT HANDLERS
           ========================================================================== */
        function initUI() {
            renderStudentSelector();
            renderCategoryList();
        }

        function renderAll() {
            renderStudentSelector();
            if (appData.activeRole === 'student') {
                renderFormulaList();
                updateGlobalProgress();
            } else {
                renderTeacherDashboard();
            }
        }

        function renderStudentSelector() {
            const select = document.getElementById('userSelect');
            select.innerHTML = appData.students.map(s => 
                `<option value="${s.id}" ${s.id === appData.activeStudentId ? 'selected' : ''}>${s.name}</option>`
            ).join('');
        }

        function changeActiveUser(newId) {
            appData.activeStudentId = newId;
            saveDataToStorage();
            renderAll();
        }

        function switchRole(role) {
            appData.activeRole = role;
            const btnStudent = document.getElementById('btnStudentMode');
            const btnTeacher = document.getElementById('btnTeacherMode');
            const studentView = document.getElementById('studentView');
            const teacherView = document.getElementById('teacherView');

            if (role === 'student') {
                btnStudent.className = "px-3 py-1.5 rounded-lg text-xs sm:text-sm font-semibold transition-all duration-200 flex items-center gap-1.5 shadow-sm bg-white text-sky-700";
                btnTeacher.className = "px-3 py-1.5 rounded-lg text-xs sm:text-sm font-semibold transition-all duration-200 text-slate-600 hover:text-slate-900 flex items-center gap-1.5";
                studentView.classList.remove('hidden');
                teacherView.classList.add('hidden');
                renderFormulaList();
                updateGlobalProgress();
            } else {
                btnTeacher.className = "px-3 py-1.5 rounded-lg text-xs sm:text-sm font-semibold transition-all duration-200 flex items-center gap-1.5 shadow-sm bg-white text-sky-700";
                btnStudent.className = "px-3 py-1.5 rounded-lg text-xs sm:text-sm font-semibold transition-all duration-200 text-slate-600 hover:text-slate-900 flex items-center gap-1.5";
                teacherView.classList.remove('hidden');
                studentView.classList.add('hidden');
                renderTeacherDashboard();
            }
        }

        function switchStudentTab(tab) {
            const tabLearnBtn = document.getElementById('tabLearnBtn');
            const tabQuizBtn = document.getElementById('tabQuizBtn');
            const studentTabLearn = document.getElementById('studentTabLearn');
            const studentTabQuiz = document.getElementById('studentTabQuiz');

            if (tab === 'learn') {
                tabLearnBtn.className = "pb-3 text-xs sm:text-sm font-bold border-b-2 border-sky-600 text-sky-600 flex items-center gap-2 transition-colors";
                tabQuizBtn.className = "pb-3 text-xs sm:text-sm font-medium border-b-2 border-transparent text-slate-500 hover:text-slate-700 flex items-center gap-2 transition-colors";
                studentTabLearn.classList.remove('hidden');
                studentTabQuiz.classList.add('hidden');
                renderFormulaList();
            } else {
                tabQuizBtn.className = "pb-3 text-xs sm:text-sm font-bold border-b-2 border-sky-600 text-sky-600 flex items-center gap-2 transition-colors";
                tabLearnBtn.className = "pb-3 text-xs sm:text-sm font-medium border-b-2 border-transparent text-slate-500 hover:text-slate-700 flex items-center gap-2 transition-colors";
                studentTabQuiz.classList.remove('hidden');
                studentTabLearn.classList.add('hidden');
            }
        }

        function renderCategoryList() {
            const container = document.getElementById('categoryList');
            container.innerHTML = CATEGORIES.map(cat => {
                const isActive = cat.id === appData.activeCategory;
                return `
                    <button onclick="selectCategory('${cat.id}')" class="w-full text-left p-2.5 rounded-xl text-xs sm:text-sm font-semibold transition-all flex items-center justify-between ${isActive ? 'bg-sky-50 text-sky-700 border border-sky-200' : 'text-slate-600 hover:bg-slate-50 border border-transparent'}">
                        <span class="flex items-center gap-2">
                            <i class="fa-solid ${cat.icon} text-slate-400 ${isActive ? 'text-sky-600' : ''}"></i>
                            ${cat.name}
                        </span>
                        <i class="fa-solid fa-chevron-right text-[10px] text-slate-300"></i>
                    </button>
                `;
            }).join('');
        }

        function selectCategory(catId) {
            appData.activeCategory = catId;
            renderCategoryList();
            renderFormulaList();
        }

        function setFilter(status) {
            appData.filterStatus = status;
            ['All', 'Unlearned', 'Learned'].forEach(st => {
                const btn = document.getElementById(`filter${st}`);
                if (st.toLowerCase() === status) {
                    btn.className = "flex-1 py-1 text-xs font-semibold rounded text-center bg-white text-slate-800 shadow-sm";
                } else {
                    btn.className = "flex-1 py-1 text-xs font-semibold rounded text-center text-slate-600 hover:text-slate-900";
                }
            });
            renderFormulaList();
        }

        /* ==========================================================================
           5. STUDENT FORMULA CHECKLIST & PROGRESS
           ========================================================================== */
        function getActiveStudent() {
            return appData.students.find(s => s.id === appData.activeStudentId) || appData.students[0];
        }

        function renderFormulaList() {
            const student = getActiveStudent();
            const currentCat = CATEGORIES.find(c => c.id === appData.activeCategory);
            const searchKeyword = document.getElementById('searchInput').value.toLowerCase().trim();

            document.getElementById('currentCategoryTitle').innerText = currentCat.name;
            document.getElementById('currentCategoryDesc').innerText = currentCat.desc;

            // Filter items
            let formulas = FORMULA_DATABASE.filter(f => f.categoryId === appData.activeCategory);

            if (searchKeyword) {
                formulas = formulas.filter(f => f.title.toLowerCase().includes(searchKeyword) || f.note.toLowerCase().includes(searchKeyword));
            }

            if (appData.filterStatus === 'learned') {
                formulas = formulas.filter(f => student.learnedFormulas.includes(f.id));
            } else if (appData.filterStatus === 'unlearned') {
                formulas = formulas.filter(f => !student.learnedFormulas.includes(f.id));
            }

            // Update category progress count
            const allCatFormulas = FORMULA_DATABASE.filter(f => f.categoryId === appData.activeCategory);
            const catLearnedCount = allCatFormulas.filter(f => student.learnedFormulas.includes(f.id)).length;
            document.getElementById('categoryProgressText').innerText = `${catLearnedCount}/${allCatFormulas.length}`;

            const grid = document.getElementById('formulaGrid');
            if (formulas.length === 0) {
                grid.innerHTML = `
                    <div class="col-span-full bg-white p-8 rounded-xl border border-dashed border-slate-300 text-center text-slate-400 space-y-2">
                        <i class="fa-solid fa-folder-open text-2xl"></i>
                        <p class="text-xs">Không tìm thấy công thức nào phù hợp.</p>
                    </div>
                `;
                return;
            }

            grid.innerHTML = formulas.map(f => {
                const isLearned = student.learnedFormulas.includes(f.id);
                return `
                    <div class="bg-white rounded-xl border transition-all duration-200 p-4 flex flex-col justify-between space-y-3 shadow-sm ${isLearned ? 'border-emerald-300 bg-emerald-50/20' : 'border-slate-200 hover:border-slate-300'}">
                        <div class="space-y-2">
                            <div class="flex justify-between items-start gap-2">
                                <span class="text-xs font-bold text-slate-800">${f.title}</span>
                                <span class="text-[10px] font-semibold px-2 py-0.5 rounded-full ${isLearned ? 'bg-emerald-100 text-emerald-700' : 'bg-slate-100 text-slate-500'}">
                                    ${isLearned ? 'Đã thuộc' : 'Chưa thuộc'}
                                </span>
                            </div>
                            <!-- Math Formula Display -->
                            <div class="py-2 px-3 bg-slate-50 rounded-lg text-center overflow-x-auto border border-slate-100 font-mono text-slate-900">
                                $$${f.latex}$$
                            </div>
                            <p class="text-[11px] text-slate-500 italic">
                                <i class="fa-solid fa-lightbulb text-amber-500 mr-1"></i>${f.note}
                            </p>
                        </div>

                        <div class="pt-2 border-t border-slate-100 flex justify-end">
                            <button onclick="toggleFormulaLearned('${f.id}')" class="px-3 py-1.5 rounded-lg text-xs font-bold transition-all flex items-center gap-1.5 ${isLearned ? 'bg-emerald-600 text-white shadow-sm hover:bg-emerald-700' : 'bg-slate-100 text-slate-700 hover:bg-slate-200'}">
                                <i class="fa-solid ${isLearned ? 'fa-check' : 'fa-plus'}"></i>
                                ${isLearned ? 'Đã thuộc bài' : 'Đánh dấu đã thuộc'}
                            </button>
                        </div>
                    </div>
                `;
            }).join('');

            triggerMathJax();
        }

        function toggleFormulaLearned(formulaId) {
            const student = getActiveStudent();
            const index = student.learnedFormulas.indexOf(formulaId);
            if (index > -1) {
                student.learnedFormulas.splice(index, 1);
            } else {
                student.learnedFormulas.push(formulaId);
            }
            saveDataToStorage();
            renderFormulaList();
            updateGlobalProgress();
        }

        function markAllInCategoryLearned() {
            const student = getActiveStudent();
            const currentCatFormulas = FORMULA_DATABASE.filter(f => f.categoryId === appData.activeCategory);
            currentCatFormulas.forEach(f => {
                if (!student.learnedFormulas.includes(f.id)) {
                    student.learnedFormulas.push(f.id);
                }
            });
            saveDataToStorage();
            renderFormulaList();
            updateGlobalProgress();
        }

        function updateGlobalProgress() {
            const student = getActiveStudent();
            const totalFormulas = FORMULA_DATABASE.length;
            const learnedCount = student.learnedFormulas.length;
            const percent = Math.round((learnedCount / totalFormulas) * 100);

            document.getElementById('globalProgressBar').style.width = `${percent}%`;
            document.getElementById('globalProgressText').innerText = `${percent}%`;
        }

        /* ==========================================================================
           6. QUIZ / TESTING SYSTEM
           ========================================================================== */
        function startQuiz() {
            // Shuffle quiz bank and pick 10 random questions
            const shuffled = [...QUIZ_BANK].sort(() => 0.5 - Math.random());
            currentQuiz = {
                questions: shuffled.slice(0, 10),
                currentIndex: 0,
                score: 0,
                selectedOption: null,
                isAnswered: false
            };

            document.getElementById('quizIntroCard').classList.add('hidden');
            document.getElementById('quizResultCard').classList.add('hidden');
            document.getElementById('quizActiveCard').classList.remove('hidden');

            renderQuizQuestion();
        }

        function renderQuizQuestion() {
            const q = currentQuiz.questions[currentQuiz.currentIndex];
            currentQuiz.selectedOption = null;
            currentQuiz.isAnswered = false;

            document.getElementById('quizCurrentNum').innerText = currentQuiz.currentIndex + 1;
            document.getElementById('quizCategoryBadge').innerText = q.category;
            document.getElementById('quizCurrentScore').innerText = `${currentQuiz.score}/10`;
            document.getElementById('quizQuestionText').innerHTML = `Câu ${currentQuiz.currentIndex + 1}: ${q.question}`;

            const container = document.getElementById('quizOptionsContainer');
            const optionLabels = ['A', 'B', 'C', 'D'];
            container.innerHTML = q.options.map((opt, idx) => `
                <button id="optBtn_${idx}" onclick="selectQuizOption(${idx})" class="w-full text-left p-3.5 rounded-xl border border-slate-200 hover:border-sky-300 hover:bg-sky-50/50 transition flex items-start gap-3 bg-white text-slate-800 text-xs sm:text-sm font-medium">
                    <span class="w-6 h-6 rounded-lg bg-slate-100 text-slate-600 font-bold flex items-center justify-center shrink-0 border border-slate-200">${optionLabels[idx]}</span>
                    <span class="pt-0.5">${opt}</span>
                </button>
            `).join('');

            // Reset explanation panel & Next button
            document.getElementById('quizExplanationPanel').classList.add('hidden');
            const nextBtn = document.getElementById('btnNextQuestion');
            nextBtn.disabled = true;
            nextBtn.className = "px-5 py-2.5 bg-slate-200 text-slate-400 font-bold rounded-xl text-xs sm:text-sm cursor-not-allowed transition flex items-center gap-2";

            triggerMathJax();
        }

        function selectQuizOption(optionIndex) {
            if (currentQuiz.isAnswered) return;

            currentQuiz.isAnswered = true;
            currentQuiz.selectedOption = optionIndex;
            const q = currentQuiz.questions[currentQuiz.currentIndex];
            const isCorrect = (optionIndex === q.correct);

            if (isCorrect) currentQuiz.score += 1;

            // Highlight options
            for (let i = 0; i < q.options.length; i++) {
                const btn = document.getElementById(`optBtn_${i}`);
                if (i === q.correct) {
                    btn.className = "w-full text-left p-3.5 rounded-xl border border-emerald-300 bg-emerald-50 text-emerald-900 font-medium text-xs sm:text-sm flex items-start gap-3";
                } else if (i === optionIndex && !isCorrect) {
                    btn.className = "w-full text-left p-3.5 rounded-xl border border-rose-300 bg-rose-50 text-rose-900 font-medium text-xs sm:text-sm flex items-start gap-3";
                } else {
                    btn.className = "w-full text-left p-3.5 rounded-xl border border-slate-200 opacity-50 bg-white text-slate-800 text-xs sm:text-sm flex items-start gap-3";
                }
            }

            // Show explanation
            const panel = document.getElementById('quizExplanationPanel');
            const badge = document.getElementById('quizResultBadge');
            const expText = document.getElementById('quizExplanationText');

            if (isCorrect) {
                panel.className = "p-4 rounded-xl border border-emerald-200 bg-emerald-50 text-xs sm:text-sm space-y-1";
                badge.className = "font-bold text-emerald-700 flex items-center gap-1.5";
                badge.innerHTML = `<i class="fa-solid fa-circle-check"></i> Chính xác! +1 điểm`;
            } else {
                panel.className = "p-4 rounded-xl border border-rose-200 bg-rose-50 text-xs sm:text-sm space-y-1";
                badge.className = "font-bold text-rose-700 flex items-center gap-1.5";
                badge.innerHTML = `<i class="fa-solid fa-circle-xmark"></i> Chưa đúng!`;
            }

            expText.innerHTML = `<strong>Giải thích:</strong> ${q.explanation}`;
            panel.classList.remove('hidden');

            // Enable Next Button
            const nextBtn = document.getElementById('btnNextQuestion');
            nextBtn.disabled = false;
            nextBtn.className = "px-5 py-2.5 bg-sky-600 text-white hover:bg-sky-700 font-bold rounded-xl text-xs sm:text-sm shadow-sm transition flex items-center gap-2 cursor-pointer";

            triggerMathJax();
        }

        function nextQuestion() {
            if (currentQuiz.currentIndex < currentQuiz.questions.length - 1) {
                currentQuiz.currentIndex++;
                renderQuizQuestion();
            } else {
                finishQuiz();
            }
        }

        function finishQuiz() {
            document.getElementById('quizActiveCard').classList.add('hidden');
            document.getElementById('quizResultCard').classList.remove('hidden');

            const score = currentQuiz.score;
            document.getElementById('quizFinalScore').innerText = `${score}/10`;

            const iconBox = document.getElementById('quizResultIcon');
            const badge = document.getElementById('quizGradeBadge');
            const advice = document.getElementById('quizAdviceText');

            if (score >= 9) {
                iconBox.className = "w-20 h-20 rounded-full bg-emerald-100 text-emerald-600 flex items-center justify-center mx-auto text-3xl font-bold shadow-sm";
                iconBox.innerHTML = '<i class="fa-solid fa-trophy"></i>';
                badge.className = "inline-block text-xs font-bold px-3 py-1 rounded-full bg-emerald-100 text-emerald-800";
                badge.innerText = "Xuất sắc";
                advice.innerText = '"Kiến thức của bạn rất vững vàng! Hãy tiếp tục duy trì phong độ đỉnh cao nhé."';
            } else if (score >= 6) {
                iconBox.className = "w-20 h-20 rounded-full bg-sky-100 text-sky-600 flex items-center justify-center mx-auto text-3xl font-bold shadow-sm";
                iconBox.innerHTML = '<i class="fa-solid fa-star"></i>';
                badge.className = "inline-block text-xs font-bold px-3 py-1 rounded-full bg-sky-100 text-sky-800";
                badge.innerText = "Khá tốt";
                advice.innerText = '"Bạn đã nắm được đa số công thức. Ôn lại các công thức chưa thuộc để đạt 10 điểm tuyệt đối!"';
            } else {
                iconBox.className = "w-20 h-20 rounded-full bg-amber-100 text-amber-600 flex items-center justify-center mx-auto text-3xl font-bold shadow-sm";
                iconBox.innerHTML = '<i class="fa-solid fa-book-bookmark"></i>';
                badge.className = "inline-block text-xs font-bold px-3 py-1 rounded-full bg-amber-100 text-amber-800";
                badge.innerText = "Cần cố gắng thêm";
                advice.innerText = '"Hãy dành thời gian tra cứu và học lại các thẻ công thức trước khi thử sức lại nhé."';
            }

            // Sync result to active student profile
            const student = getActiveStudent();
            const today = new Date().toISOString().split('T')[0];
            student.quizHistory.push({
                date: today,
                score: score,
                total: 10
            });
            saveDataToStorage();
        }

        /* ==========================================================================
           7. TEACHER MODE DASHBOARD & MANAGEMENT
           ========================================================================== */
        function renderTeacherDashboard() {
            const students = appData.students;
            const totalFormulasCount = FORMULA_DATABASE.length;

            // Stats Calculations
            const totalStudents = students.length;
            let totalLearnedCount = 0;
            let totalQuizScores = 0;
            let totalQuizAttempts = 0;
            let passedStudentsCount = 0;

            students.forEach(s => {
                totalLearnedCount += s.learnedFormulas.length;
                if (s.quizHistory.length > 0) {
                    const avgScore = s.quizHistory.reduce((acc, q) => acc + q.score, 0) / s.quizHistory.length;
                    totalQuizScores += avgScore;
                    totalQuizAttempts += 1;
                    if (avgScore >= 5.0) passedStudentsCount++;
                }
            });

            const overallClassAvg = totalQuizAttempts > 0 ? (totalQuizScores / totalQuizAttempts).toFixed(1) : '0.0';
            const passRate = totalQuizAttempts > 0 ? Math.round((passedStudentsCount / totalQuizAttempts) * 100) : 0;

            document.getElementById('statTotalStudents').innerText = totalStudents;
            document.getElementById('statTotalLearned').innerText = totalLearnedCount;
            document.getElementById('statAverageScore').innerText = overallClassAvg;
            document.getElementById('statPassRate').innerText = `${passRate}%`;

            // Table Rendering
            const tableBody = document.getElementById('teacherStudentTable');
            tableBody.innerHTML = students.map(s => {
                const learnedCount = s.learnedFormulas.length;
                const learnedPercent = Math.round((learnedCount / totalFormulasCount) * 100);
                const quizCount = s.quizHistory.length;
                const avgScore = quizCount > 0 ? (s.quizHistory.reduce((a, b) => a + b.score, 0) / quizCount).toFixed(1) : 'N/A';

                // Evaluation badge
                let evalBadge = `<span class="px-2.5 py-1 rounded-full text-[11px] font-bold bg-slate-100 text-slate-600">Chưa kiểm tra</span>`;
                if (avgScore !== 'N/A') {
                    const scoreNum = parseFloat(avgScore);
                    if (scoreNum >= 8.5 && learnedPercent >= 70) {
                        evalBadge = `<span class="px-2.5 py-1 rounded-full text-[11px] font-bold bg-emerald-100 text-emerald-800"><i class="fa-solid fa-shield-check mr-1"></i>Thuộc bài tốt</span>`;
                    } else if (scoreNum >= 5.0) {
                        evalBadge = `<span class="px-2.5 py-1 rounded-full text-[11px] font-bold bg-sky-100 text-sky-800"><i class="fa-solid fa-circle-check mr-1"></i>Đạt yêu cầu</span>`;
                    } else {
                        evalBadge = `<span class="px-2.5 py-1 rounded-full text-[11px] font-bold bg-rose-100 text-rose-800"><i class="fa-solid fa-triangle-exclamation mr-1"></i>Cần hỗ trợ</span>`;
                    }
                }

                return `
                    <tr class="hover:bg-slate-50/80 transition-colors">
                        <td class="py-3.5 px-4 font-bold text-slate-800">
                            ${s.name}
                            ${s.id === appData.activeStudentId ? '<span class="ml-1 text-[10px] bg-sky-100 text-sky-700 px-1.5 py-0.5 rounded">Hiện tại</span>' : ''}
                        </td>
                        <td class="py-3.5 px-4">
                            <div class="flex items-center gap-2">
                                <span class="font-bold text-slate-700">${learnedCount}/${totalFormulasCount}</span>
                                <div class="w-16 bg-slate-100 rounded-full h-1.5 overflow-hidden">
                                    <div class="bg-emerald-500 h-1.5 rounded-full" style="width: ${learnedPercent}%"></div>
                                </div>
                                <span class="text-xs text-slate-400">(${learnedPercent}%)</span>
                            </div>
                        </td>
                        <td class="py-3.5 px-4 text-center font-semibold text-slate-600">${quizCount}</td>
                        <td class="py-3.5 px-4 text-center">
                            <span class="font-bold ${avgScore >= 8 ? 'text-emerald-600' : avgScore >= 5 ? 'text-sky-600' : avgScore === 'N/A' ? 'text-slate-400' : 'text-rose-600'}">
                                ${avgScore}
                            </span>
                        </td>
                        <td class="py-3.5 px-4">${evalBadge}</td>
                        <td class="py-3.5 px-4 text-right">
                            <button onclick="resetStudentProgress('${s.id}')" title="Đặt lại dữ liệu học sinh này" class="p-1.5 text-slate-400 hover:text-rose-600 rounded-lg hover:bg-rose-50 transition">
                                <i class="fa-solid fa-rotate-left"></i>
                            </button>
                        </td>
                    </tr>
                `;
            }).join('');
        }

        /* ==========================================================================
           8. MODAL & USER ACTIONS
           ========================================================================== */
        function showAddStudentModal() {
            document.getElementById('newStudentName').value = '';
            document.getElementById('addStudentModal').classList.remove('hidden');
        }

        function closeAddStudentModal() {
            document.getElementById('addStudentModal').classList.add('hidden');
        }

        function saveNewStudent() {
            const nameInput = document.getElementById('newStudentName').value.trim();
            if (!nameInput) return;

            const newStudent = {
                id: 'stu_' + Date.now(),
                name: nameInput,
                learnedFormulas: [],
                quizHistory: []
            };

            appData.students.push(newStudent);
            appData.activeStudentId = newStudent.id;
            saveDataToStorage();
            closeAddStudentModal();
            renderAll();
        }

        function resetStudentProgress(studentId) {
            const student = appData.students.find(s => s.id === studentId);
            if (!student) return;

            showConfirmModal(
                'Đặt lại tiến độ?',
                `Bạn có chắc chắn muốn xóa tất cả công thức đã thuộc và lịch sử thi của "${student.name}"?`,
                () => {
                    student.learnedFormulas = [];
                    student.quizHistory = [];
                    saveDataToStorage();
                    renderAll();
                }
            );
        }

        function confirmResetAllData() {
            showConfirmModal(
                'Khôi phục dữ liệu gốc?',
                'Hành động này sẽ xóa toàn bộ dữ liệu hiện tại và khôi phục về danh sách 4 học sinh mặc định ban đầu.',
                () => {
                    appData.students = JSON.parse(JSON.stringify(INITIAL_STUDENTS));
                    appData.activeStudentId = 'stu_1';
                    saveDataToStorage();
                    renderAll();
                }
            );
        }

        function showConfirmModal(title, message, onConfirm) {
            document.getElementById('confirmTitle').innerText = title;
            document.getElementById('confirmMessage').innerText = message;
            const btnConfirm = document.getElementById('btnConfirmAction');

            btnConfirm.onclick = () => {
                onConfirm();
                closeConfirmModal();
            };

            document.getElementById('confirmModal').classList.remove('hidden');
        }

        function closeConfirmModal() {
            document.getElementById('confirmModal').classList.add('hidden');
        }
    </script>
</body>
</html>
