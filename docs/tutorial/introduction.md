<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>برنامج إدارة عملاء الترزي (مع تحليل ذكي)</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Cairo', sans-serif;
        }
        /* Custom scrollbar for better look */
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #f1f1f1;
        }
        ::-webkit-scrollbar-thumb {
            background: #888;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #555;
        }
        .toast {
            visibility: hidden;
            min-width: 250px;
            margin-left: -125px;
            background-color: #333;
            color: #fff;
            text-align: center;
            border-radius: 8px;
            padding: 16px;
            position: fixed;
            z-index: 100;
            left: 50%;
            bottom: 30px;
            opacity: 0;
            transition: visibility 0s, opacity 0.5s linear;
        }
        .toast.show {
            visibility: visible;
            opacity: 1;
        }
        .loader {
            border: 4px solid #f3f3f3;
            border-radius: 50%;
            border-top: 4px solid #3498db;
            width: 24px;
            height: 24px;
            -webkit-animation: spin 2s linear infinite; /* Safari */
            animation: spin 2s linear infinite;
        }
        @-webkit-keyframes spin {
          0% { -webkit-transform: rotate(0deg); }
          100% { -webkit-transform: rotate(360deg); }
        }
        @keyframes spin {
          0% { transform: rotate(0deg); }
          100% { transform: rotate(360deg); }
        }
        /* Add focus styles to input fields */
        input[type="text"]:focus, input[type="tel"]:focus, input[type="number"]:focus, textarea:focus {
             border-color: #3b82f6;
             box-shadow: 0 0 0 2px rgba(59, 130, 246, 0.5);
             outline: none;
        }
    </style>
</head>
<body class="bg-gray-100">

    <div class="container mx-auto p-4 sm:p-6 md:p-8 max-w-5xl">
        <header class="text-center mb-8">
            <h1 class="text-3xl md:text-4xl font-bold text-gray-800">برنامج إدارة عملاء الترزي</h1>
            <p class="text-gray-600 mt-2">أضف، ابحث، وعدّل بيانات عملائك مع مساعدة ذكية ✨</p>
        </header>

        <!-- Form for adding and editing customers -->
        <div class="bg-white p-6 rounded-lg shadow-md mb-8">
            <h2 id="form-title" class="text-2xl font-semibold text-gray-700 mb-6">إضافة عميل جديد</h2>
            <form id="customer-form" class="space-y-6">
                <input type="hidden" id="customer-id">
                
                <!-- Basic Info -->
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <div>
                        <label for="name" class="block text-sm font-medium text-gray-700 mb-1">اسم العميل</label>
                        <input type="text" id="name" placeholder="مثال: محمد عبدالله" required class="w-full px-4 py-2 border border-gray-300 rounded-lg transition">
                    </div>
                    <div>
                        <label for="phone" class="block text-sm font-medium text-gray-700 mb-1">رقم الهاتف</label>
                        <input type="tel" id="phone" placeholder="مثال: 05xxxxxxx" required class="w-full px-4 py-2 border border-gray-300 rounded-lg transition">
                    </div>
                </div>

                <!-- Measurements -->
                <fieldset class="border border-gray-300 rounded-lg p-4">
                    <legend class="text-lg font-semibold text-gray-700 px-2">القياسات</legend>
                    <div class="grid grid-cols-2 md:grid-cols-4 gap-x-4 gap-y-5 mt-4">
                        <div>
                            <label for="m-length" class="block text-sm font-medium text-gray-700 mb-1">الطول</label>
                            <input type="number" step="0.1" id="m-length" placeholder="0" class="w-full px-3 py-2 border border-gray-300 rounded-lg transition">
                        </div>
                         <div>
                            <label for="m-width" class="block text-sm font-medium text-gray-700 mb-1">العرض</label>
                            <input type="number" step="0.1" id="m-width" placeholder="0" class="w-full px-3 py-2 border border-gray-300 rounded-lg transition">
                        </div>
                        <div>
                            <label for="m-body" class="block text-sm font-medium text-gray-700 mb-1">بدن</label>
                            <input type="number" step="0.1" id="m-body" placeholder="0" class="w-full px-3 py-2 border border-gray-300 rounded-lg transition">
                        </div>
                        <div>
                            <label for="m-sleeve-length" class="block text-sm font-medium text-gray-700 mb-1">طول كم</label>
                            <input type="number" step="0.1" id="m-sleeve-length" placeholder="0" class="w-full px-3 py-2 border border-gray-300 rounded-lg transition">
                        </div>
                         <div>
                            <label for="m-sleeve-width" class="block text-sm font-medium text-gray-700 mb-1">عرض كم</label>
                            <input type="number" step="0.1" id="m-sleeve-width" placeholder="0" class="w-full px-3 py-2 border border-gray-300 rounded-lg transition">
                        </div>
                        <div>
                            <label for="m-khazna" class="block text-sm font-medium text-gray-700 mb-1">خزنة</label>
                            <input type="number" step="0.1" id="m-khazna" placeholder="0" class="w-full px-3 py-2 border border-gray-300 rounded-lg transition">
                        </div>
                        <div>
                            <label for="m-collar" class="block text-sm font-medium text-gray-700 mb-1">قب</label>
                            <input type="number" step="0.1" id="m-collar" placeholder="0" class="w-full px-3 py-2 border border-gray-300 rounded-lg transition">
                        </div>
                        <div>
                            <label for="m-collar-length" class="block text-sm font-medium text-gray-700 mb-1">طول قب</label>
                            <input type="number" step="0.1" id="m-collar-length" placeholder="0" class="w-full px-3 py-2 border border-gray-300 rounded-lg transition">
                        </div>
                    </div>
                    <div class="mt-5">
                         <div class="flex justify-between items-center mb-1">
                            <label for="m-details" class="block text-sm font-medium text-gray-700">تفاصيل إضافية</label>
                            <button type="button" id="analyze-details-btn" class="text-sm text-blue-600 hover:text-blue-800 font-semibold flex items-center gap-1">
                                ✨ تحليل التفاصيل
                                <span id="analyze-loader" class="hidden loader !w-4 !h-4 !border-2"></span>
                            </button>
                         </div>
                         <textarea id="m-details" rows="3" placeholder="اكتب هنا أي ملاحظات أو تفاصيل أخرى..." class="w-full px-4 py-2 border border-gray-300 rounded-lg transition"></textarea>
                    </div>
                </fieldset>

                <div class="flex items-center justify-end space-x-4 space-x-reverse pt-2">
                    <button type="button" id="cancel-edit-btn" class="hidden px-6 py-2 bg-gray-500 text-white font-semibold rounded-lg shadow-md hover:bg-gray-600 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-gray-500 transition">إلغاء التعديل</button>
                    <button type="submit" id="submit-btn" class="px-6 py-2 bg-blue-600 text-white font-semibold rounded-lg shadow-md hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-600 transition">إضافة العميل</button>
                </div>
            </form>
        </div>

        <!-- Search and display area -->
        <div class="bg-white p-6 rounded-lg shadow-md">
            <h2 class="text-2xl font-semibold text-gray-700 mb-4">قائمة العملاء</h2>
            <div class="mb-4">
                 <input type="text" id="search" placeholder="ابحث بالاسم أو رقم الهاتف..." class="w-full px-4 py-2 border border-gray-300 rounded-lg transition">
            </div>
            
            <div class="mb-4 p-2 bg-blue-50 border border-blue-200 rounded-lg text-center">
                <p class="text-sm text-blue-700">معرّف المستخدم الخاص بك (للمشاركة): <strong id="user-id-display" class="font-mono"></strong></p>
            </div>
            
            <div id="customer-list" class="space-y-4">
                <div id="loading-state" class="text-center py-8">
                    <p class="text-gray-500">جاري تحميل البيانات...</p>
                </div>
            </div>
        </div>
    </div>
    
    <!-- Toast Notification -->
    <div id="toast" class="toast"></div>

    <!-- Modals -->
    <div id="delete-modal" class="hidden fixed inset-0 bg-black bg-opacity-50 z-50 flex justify-center items-center p-4">
        <div class="bg-white rounded-lg p-8 shadow-2xl w-full max-w-sm">
            <h3 class="text-xl font-bold text-gray-900 mb-4">تأكيد الحذف</h3>
            <p class="text-gray-600 mb-6">هل أنت متأكد من أنك تريد حذف هذا العميل؟ لا يمكن التراجع عن هذا الإجراء.</p>
            <div class="flex justify-end space-x-4 space-x-reverse">
                <button id="cancel-delete-btn" class="px-4 py-2 bg-gray-300 text-gray-800 rounded-lg hover:bg-gray-400 transition">إلغاء</button>
                <button id="confirm-delete-btn" class="px-4 py-2 bg-red-600 text-white rounded-lg hover:bg-red-700 transition">نعم، احذف</button>
            </div>
        </div>
    </div>

    <div id="sms-modal" class="hidden fixed inset-0 bg-black bg-opacity-50 z-50 flex justify-center items-center p-4">
        <div class="bg-white rounded-lg p-8 shadow-2xl w-full max-w-md">
            <h3 class="text-xl font-bold text-gray-900 mb-4">✨ رسالة جاهزة</h3>
            <div id="sms-content" class="mb-6 p-4 bg-gray-100 rounded-lg text-gray-700 whitespace-pre-wrap min-h-[100px] flex justify-center items-center">
                 <div class="loader"></div>
            </div>
            <div class="flex justify-between items-center">
                <button id="copy-sms-btn" class="px-4 py-2 bg-green-600 text-white rounded-lg hover:bg-green-700 transition">نسخ النص</button>
                <button id="close-sms-modal-btn" class="px-4 py-2 bg-gray-300 text-gray-800 rounded-lg hover:bg-gray-400 transition">إغلاق</button>
            </div>
        </div>
    </div>
    
    <div id="analysis-modal" class="hidden fixed inset-0 bg-black bg-opacity-50 z-50 flex justify-center items-center p-4">
        <div class="bg-white rounded-lg p-8 shadow-2xl w-full max-w-md">
            <h3 class="text-xl font-bold text-gray-900 mb-4">✨ تحليل التفاصيل واقتراحات</h3>
            <div id="analysis-content" class="mb-6 p-4 bg-gray-100 rounded-lg text-gray-700 whitespace-pre-wrap min-h-[120px] flex justify-center items-center">
                 <div class="loader"></div>
            </div>
            <div class="flex justify-end">
                <button id="close-analysis-modal-btn" class="px-4 py-2 bg-gray-300 text-gray-800 rounded-lg hover:bg-gray-400 transition">إغلاق</button>
            </div>
        </div>
    </div>


    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, signInAnonymously, signInWithCustomToken, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, collection, doc, addDoc, onSnapshot, updateDoc, deleteDoc, query } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

        // --- CONFIGURATION ---
        const firebaseConfig = typeof __firebase_config !== 'undefined' ? JSON.parse(__firebase_config) : { apiKey: "DEMO", authDomain: "DEMO", projectId: "DEMO" };
        const appId = typeof __app_id !== 'undefined' ? __app_id : 'default-tailor-app';

        // --- INITIALIZATION ---
        const app = initializeApp(firebaseConfig);
        const auth = getAuth(app);
        const db = getFirestore(app);
        
        let userId = null;
        let customersCollectionRef = null;
        let unsubscribe = null; 
        let allCustomers = []; // To hold the full customer data for editing

        // To translate measurement keys to Arabic labels
        const measurementLabels = {
            length: "الطول",
            width: "العرض",
            body: "بدن",
            sleeveLength: "طول كم",
            sleeveWidth: "عرض كم",
            khazna: "خزنة",
            collar: "قب",
            collarLength: "طول قب",
            details: "تفاصيل"
        };

        // --- UI ELEMENTS ---
        const customerForm = document.getElementById('customer-form');
        const customerIdInput = document.getElementById('customer-id');
        const nameInput = document.getElementById('name');
        const phoneInput = document.getElementById('phone');
        
        // Measurement Inputs
        const measurementInputs = {
            length: document.getElementById('m-length'),
            width: document.getElementById('m-width'),
            body: document.getElementById('m-body'),
            sleeveLength: document.getElementById('m-sleeve-length'),
            sleeveWidth: document.getElementById('m-sleeve-width'),
            khazna: document.getElementById('m-khazna'),
            collar: document.getElementById('m-collar'),
            collarLength: document.getElementById('m-collar-length'),
            details: document.getElementById('m-details'),
        };
        
        const submitBtn = document.getElementById('submit-btn');
        const cancelEditBtn = document.getElementById('cancel-edit-btn');
        const formTitle = document.getElementById('form-title');
        const customerList = document.getElementById('customer-list');
        const loadingState = document.getElementById('loading-state');
        const searchInput = document.getElementById('search');
        const toast = document.getElementById('toast');
        const deleteModal = document.getElementById('delete-modal');
        const confirmDeleteBtn = document.getElementById('confirm-delete-btn');
        const cancelDeleteBtn = document.getElementById('cancel-delete-btn');
        const userIdDisplay = document.getElementById('user-id-display');
        
        // Gemini Feature Elements
        const smsModal = document.getElementById('sms-modal');
        const smsContent = document.getElementById('sms-content');
        const copySmsBtn = document.getElementById('copy-sms-btn');
        const closeSmsModalBtn = document.getElementById('close-sms-modal-btn');
        const analyzeDetailsBtn = document.getElementById('analyze-details-btn');
        const analyzeLoader = document.getElementById('analyze-loader');
        const analysisModal = document.getElementById('analysis-modal');
        const analysisContent = document.getElementById('analysis-content');
        const closeAnalysisModalBtn = document.getElementById('close-analysis-modal-btn');


        let customerToDeleteId = null;

        // --- AUTHENTICATION ---
        onAuthStateChanged(auth, async (user) => {
            if (user) {
                userId = user.uid;
                userIdDisplay.textContent = userId;
                customersCollectionRef = collection(db, `artifacts/${appId}/users/${userId}/customers`);
                listenForCustomers();
            } else {
                userIdDisplay.textContent = '...جاري المصادقة';
                try {
                     if (typeof __initial_auth_token !== 'undefined' && __initial_auth_token) {
                        await signInWithCustomToken(auth, __initial_auth_token);
                    } else {
                        await signInAnonymously(auth);
                    }
                } catch (error) {
                    console.error("Error during sign-in:", error);
                    userIdDisplay.textContent = 'فشل في المصادقة';
                }
            }
        });


        // --- FIRESTORE REAL-TIME LISTENER ---
        function listenForCustomers() {
            if (unsubscribe) unsubscribe();
            if (!customersCollectionRef) return;

            const q = query(customersCollectionRef);
            unsubscribe = onSnapshot(q, (querySnapshot) => {
                const customers = [];
                querySnapshot.forEach((doc) => customers.push({ id: doc.id, ...doc.data() }));
                customers.sort((a, b) => a.name.localeCompare(b.name, 'ar'));
                allCustomers = customers; // Store for easy access
                renderCustomers(customers);
            }, (error) => {
                console.error("Error fetching customers: ", error);
                customerList.innerHTML = `<div class="text-center py-8 text-red-500">لا يمكن تحميل البيانات. تحقق من اتصالك بالإنترنت.</div>`;
            });
        }

        // --- RENDERING ---
        function renderCustomers(customers) {
            loadingState.style.display = 'none';
            customerList.innerHTML = ''; 

            if (customers.length === 0) {
                customerList.innerHTML = `<div class="text-center py-8"><p class="text-gray-500">لم يتم إضافة أي عملاء بعد. ابدأ بإضافة عميل جديد!</p></div>`;
                return;
            }

            const searchQuery = searchInput.value.toLowerCase();
            const filteredCustomers = customers.filter(c => c.name.toLowerCase().includes(searchQuery) || c.phone.includes(searchQuery));

            filteredCustomers.forEach(customer => {
                const card = document.createElement('div');
                card.className = 'customer-card bg-gray-50 p-5 rounded-lg border border-gray-200 flex flex-col sm:flex-row justify-between items-start gap-4 transition-shadow hover:shadow-md';
                card.dataset.id = customer.id;

                // Create measurements display
                let measurementsHtml = '<p class="text-gray-500">لا توجد قياسات مسجلة.</p>';
                if (customer.measurements && Object.values(customer.measurements).some(v => v)) {
                    measurementsHtml = Object.entries(customer.measurements)
                        .filter(([_, value]) => value) // Only show fields with a value
                        .map(([key, value]) => `
                            <span class="inline-block bg-gray-200 rounded px-2 py-1 text-sm text-gray-700">
                                <strong>${measurementLabels[key] || key}:</strong> ${escapeHTML(value)}
                            </span>
                        `)
                        .join(' ');
                }

                card.innerHTML = `
                    <div class="flex-grow">
                        <h3 class="text-lg font-bold text-gray-800">${escapeHTML(customer.name)}</h3>
                        <p class="text-gray-600 font-mono mb-3">${escapeHTML(customer.phone)}</p>
                        <div class="flex flex-wrap gap-2">
                           ${measurementsHtml}
                        </div>
                    </div>
                    <div class="flex flex-col gap-2 self-start flex-shrink-0 w-full sm:w-auto">
                        <button class="sms-btn w-full px-3 py-1.5 bg-teal-500 text-white text-sm font-semibold rounded-md hover:bg-teal-600 transition" data-name="${escapeHTML(customer.name)}">✨ إنشاء رسالة</button>
                        <button class="edit-btn w-full px-3 py-1.5 bg-yellow-500 text-white text-sm font-semibold rounded-md hover:bg-yellow-600 transition" data-id="${customer.id}">تعديل</button>
                        <button class="delete-btn w-full px-3 py-1.5 bg-red-500 text-white text-sm font-semibold rounded-md hover:bg-red-600 transition" data-id="${customer.id}">حذف</button>
                    </div>
                `;
                customerList.appendChild(card);
            });
        }

        // --- FORM HANDLING ---
        customerForm.addEventListener('submit', async (e) => {
            e.preventDefault();
            if (!customersCollectionRef) {
                showToast("خطأ: لم يتم تهيئة قاعدة البيانات.", true);
                return;
            }

            const id = customerIdInput.value;
            const customerMeasurements = {};
            for (const key in measurementInputs) {
                customerMeasurements[key] = measurementInputs[key].value.trim();
            }

            const customerData = {
                name: nameInput.value.trim(),
                phone: phoneInput.value.trim(),
                measurements: customerMeasurements,
            };

            if (!customerData.name || !customerData.phone) {
                showToast("الرجاء إدخال الاسم ورقم الهاتف.", true);
                return;
            }

            try {
                if (id) {
                    await updateDoc(doc(customersCollectionRef, id), customerData);
                    showToast("تم تحديث بيانات العميل بنجاح.");
                } else {
                    await addDoc(customersCollectionRef, customerData);
                    showToast("تمت إضافة العميل بنجاح.");
                }
                resetForm();
            } catch (error) {
                console.error("Error saving customer: ", error);
                showToast("حدث خطأ أثناء حفظ البيانات.", true);
            }
        });
        
        function resetForm() {
            customerForm.reset();
            customerIdInput.value = '';
            formTitle.textContent = 'إضافة عميل جديد';
            submitBtn.textContent = 'إضافة العميل';
            cancelEditBtn.classList.add('hidden');
        }

        // --- EVENT LISTENERS ---
        customerList.addEventListener('click', (e) => {
            const target = e.target.closest('button');
            if (!target) return;

            if (target.classList.contains('edit-btn')) {
                const customerToEdit = allCustomers.find(c => c.id === target.dataset.id);
                if (!customerToEdit) return;

                formTitle.textContent = 'تعديل بيانات العميل';
                submitBtn.textContent = 'حفظ التعديلات';
                customerIdInput.value = customerToEdit.id;
                nameInput.value = customerToEdit.name;
                phoneInput.value = customerToEdit.phone;

                // Populate measurement fields
                for(const key in measurementInputs) {
                    measurementInputs[key].value = customerToEdit.measurements?.[key] || '';
                }

                cancelEditBtn.classList.remove('hidden');
                window.scrollTo({ top: 0, behavior: 'smooth' });
                nameInput.focus();

            } else if (target.classList.contains('delete-btn')) {
                customerToDeleteId = target.dataset.id;
                deleteModal.classList.remove('hidden');
            } else if (target.classList.contains('sms-btn')) {
                handleSmsGeneration(target.dataset.name);
            }
        });

        cancelEditBtn.addEventListener('click', resetForm);
        searchInput.addEventListener('input', () => renderCustomers(allCustomers));

        // --- MODAL AND TOAST LOGIC ---
        function showToast(message, isError = false) {
            toast.textContent = message;
            toast.className = `toast show ${isError ? 'bg-red-600' : 'bg-green-600'}`;
            setTimeout(() => { toast.className = toast.className.replace("show", ""); }, 3000);
        }

        cancelDeleteBtn.addEventListener('click', () => {
            deleteModal.classList.add('hidden');
            customerToDeleteId = null;
        });
        
        confirmDeleteBtn.addEventListener('click', async () => {
             if (customerToDeleteId && customersCollectionRef) {
                try {
                    await deleteDoc(doc(customersCollectionRef, customerToDeleteId));
                    showToast("تم حذف العميل بنجاح.");
                } catch (error) {
                    showToast("حدث خطأ أثناء الحذف.", true);
                } finally {
                    deleteModal.classList.add('hidden');
                    customerToDeleteId = null;
                }
             }
        });
        
        closeSmsModalBtn.addEventListener('click', () => smsModal.classList.add('hidden'));
        closeAnalysisModalBtn.addEventListener('click', () => analysisModal.classList.add('hidden'));

        // --- GEMINI API FEATURES ---

        async function callGemini(prompt) {
            const apiKey = ""; // Canvas provides the key
            const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent?key=${apiKey}`;
            const payload = { contents: [{ role: "user", parts: [{ text: prompt }] }] };

            try {
                const response = await fetch(apiUrl, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(payload)
                });
                if (!response.ok) throw new Error(`API call failed with status: ${response.status}`);
                const result = await response.json();
                if (result.candidates?.[0]?.content?.parts?.[0]) {
                    return result.candidates[0].content.parts[0].text.trim();
                }
                throw new Error("Invalid response structure from API.");
            } catch (error) {
                console.error("Gemini API Error:", error);
                showToast("حدث خطأ أثناء الاتصال بالمساعد الذكي.", true);
                return null;
            }
        }

        async function handleSmsGeneration(customerName) {
            smsModal.classList.remove('hidden');
            smsContent.innerHTML = `<div class="loader"></div>`;
            copySmsBtn.disabled = true;

            const prompt = `اكتب رسالة SMS قصيرة وودودة جدًا باللغة العربية، لإعلام العميل "${customerName}" بأن طلبه لدى الخياط أصبح جاهزًا للاستلام. اجعل الرسالة احترافية ومختصرة.`;
            const smsText = await callGemini(prompt);

            if (smsText) {
                smsContent.textContent = smsText;
                copySmsBtn.disabled = false;
            } else {
                smsContent.textContent = "فشل في إنشاء الرسالة. يرجى المحاولة مرة أخرى.";
            }
        }

        analyzeDetailsBtn.addEventListener('click', async () => {
            const detailsText = measurementInputs.details.value.trim();
            if(!detailsText) {
                showToast("الرجاء كتابة بعض التفاصيل أولاً.", true);
                return;
            }

            analysisModal.classList.remove('hidden');
            analysisContent.innerHTML = `<div class="loader"></div>`;
            analyzeLoader.classList.remove('hidden');
            analyzeDetailsBtn.disabled = true;

            const prompt = `أنا خياط، وهذا ما كتبه العميل في خانة "التفاصيل الإضافية" لطلبه. مهمتك هي تحليل هذا النص واقتراح أسئلة توضيحية محددة كنقاط يجب أن أطرحها على العميل لأفهم طلبه بشكل كامل ودقيق. إذا كان النص واضحًا ولا يحتاج لأسئلة, أجب بـ "التفاصيل واضحة ومفهومة.". ركز على أي غموض أو نقص في المعلومات. لا تضف أي مقدمات أو خواتيم. النص هو: "${detailsText}"`;

            const analysisResult = await callGemini(prompt);
            
            if (analysisResult) {
                analysisContent.textContent = analysisResult;
            } else {
                analysisContent.textContent = "فشل في تحليل التفاصيل. يرجى المحاولة مرة أخرى.";
            }
            
            analyzeLoader.classList.add('hidden');
            analyzeDetailsBtn.disabled = false;
        });
        
        copySmsBtn.addEventListener('click', () => {
            const textToCopy = smsContent.textContent;
            const textArea = document.createElement('textarea');
            textArea.value = textToCopy;
            document.body.appendChild(textArea);
            textArea.select();
            try {
                 document.execCommand('copy');
                 showToast("تم نسخ النص بنجاح!");
            } catch (err) {
                 showToast("فشل النسخ. يرجى النسخ يدويًا.", true);
            }
            document.body.removeChild(textArea);
        });

        // Simple HTML sanitizer
        function escapeHTML(str) {
            if (str === null || str === undefined) return '';
            const p = document.createElement('p');
            p.appendChild(document.createTextNode(str));
            return p.innerHTML;
        }

    </script>
</body>
</html>
