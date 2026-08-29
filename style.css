/* =========================================================

1. GLOBAL STATE & LOCAL STORAGE
   ========================================================= */

let currentUser =
JSON.parse(localStorage.getItem('app_current_user')) || null;

let usersList =
JSON.parse(localStorage.getItem('app_users_list')) || [];

let appContents =
JSON.parse(localStorage.getItem('app_contents')) || [
{
id: Date.now(),
section: 'news',
title: 'مرحباً بكم في منصة مستر أشرف بسيوني التعليمية!',
link: '',
fileData: '',
fileType: '',
date: new Date().toLocaleDateString('ar-EG')
}
];

let selectedGender = '';
let isDarkMode = true;

const ADMIN_PASSWORD_DEFAULT = '1122334455';

let adminQuestionCount = 0;
let currentQuiz = null;
let quizTimerInterval = null;
let quizRemainingSeconds = 0;

/* =========================================================
2. INITIALIZATION
========================================================= */

document.addEventListener('DOMContentLoaded', () => {

initTypingEffect();

normalizeContents();

renderAllContents();

updateAllNotificationBadges();

if (currentUser) {
    showMainApp();
}

});

/* =========================================================
3. NORMALIZE OLD DATA
========================================================= */

function normalizeContents() {

let changed = false;

appContents = appContents.map(item => {

    if (!item.id) {
        item.id = Date.now() + Math.floor(Math.random() * 1000);
        changed = true;
    }

    if (!item.date) {
        item.date = new Date().toLocaleDateString('ar-EG');
        changed = true;
    }

    return item;

});

if (changed) {
    saveContents();
}

}

function saveContents() {

localStorage.setItem(
    'app_contents',
    JSON.stringify(appContents)
);

}

function saveUsers() {

localStorage.setItem(
    'app_users_list',
    JSON.stringify(usersList)
);

}

/* =========================================================
4. INTRO SCREEN & TYPING EFFECT
========================================================= */

function initTypingEffect() {

const textContainer =
    document.getElementById('typing-text');

if (!textContainer) return;

const phrases = [

    'WELCOME TO MR. ASHRAF BASSIOUNY PLATFORM',

    'SKILL UP CENTER - EXCELLENCE IN ENGLISH',

    'طريقك للتميز والتفوق في اللغة الإنجليزية'

];

let phraseIdx = 0;

let charIdx = 0;

let isDeleting = false;


function type() {

    const currentPhrase =
        phrases[phraseIdx];


    if (isDeleting) {

        textContainer.textContent =
            currentPhrase.substring(
                0,
                charIdx - 1
            );

        charIdx--;

    } else {

        textContainer.textContent =
            currentPhrase.substring(
                0,
                charIdx + 1
            );

        charIdx++;

    }


    let typeSpeed =
        isDeleting ? 35 : 70;


    if (
        !isDeleting &&
        charIdx === currentPhrase.length
    ) {

        typeSpeed = 1800;

        isDeleting = true;

    }

    else if (
        isDeleting &&
        charIdx === 0
    ) {

        isDeleting = false;

        phraseIdx =
            (phraseIdx + 1) %
            phrases.length;

        typeSpeed = 400;

    }


    setTimeout(
        type,
        typeSpeed
    );

}


type();

}

/* =========================================================
5. USER REGISTRATION
========================================================= */

function setGenderChoice(gender) {

selectedGender = gender;

const btnMale =
    document.getElementById(
        'btn-gender-male'
    );

const btnFemale =
    document.getElementById(
        'btn-gender-female'
    );


if (gender === 'male') {

    btnMale.classList.add(
        'active-male'
    );

    btnMale.classList.add(
        'bg-blue-500/20',
        'border-blue-500'
    );


    btnFemale.classList.remove(
        'active-female'
    );

    btnFemale.classList.remove(
        'bg-pink-500/20',
        'border-pink-500'
    );

}


else {

    btnFemale.classList.add(
        'active-female'
    );

    btnFemale.classList.add(
        'bg-pink-500/20',
        'border-pink-500'
    );


    btnMale.classList.remove(
        'active-male'
    );

    btnMale.classList.remove(
        'bg-blue-500/20',
        'border-blue-500'
    );

}

}

function handleRegister(event) {

event.preventDefault();


const name =
    document
        .getElementById('reg-name')
        .value
        .trim();


const phone =
    document
        .getElementById('reg-phone')
        .value
        .trim();


const grade =
    document
        .getElementById('reg-grade')
        .value;


const school =
    document
        .getElementById('reg-school')
        .value;


const pass =
    document
        .getElementById('reg-pass')
        .value;


if (!name || !phone || !grade || !school || !pass) {

    alert(
        'يرجى استكمال جميع البيانات.'
    );

    return;

}


if (!selectedGender) {

    alert(
        'يرجى تحديد النوع (طالب / طالبة).'
    );

    return;

}


const existingUser =
    usersList.find(
        user => user.phone === phone
    );


if (existingUser) {

    if (
        existingUser.pass === pass
    ) {

        currentUser = existingUser;

    }

    else {

        alert(
            'رقم الهاتف مسجل بالفعل وكلمة المرور غير صحيحة.'
        );

        return;

    }

}


else {

    currentUser = {

        id:
            Date.now(),

        name,

        phone,

        grade,

        school,

        pass,

        gender:
            selectedGender,

        message:
            '',

        reply:
            ''

    };


    usersList.push(
        currentUser
    );


    saveUsers();

}


localStorage.setItem(
    'app_current_user',
    JSON.stringify(currentUser)
);


showMainApp();

}

/* =========================================================
6. MAIN APPLICATION
========================================================= */

function showMainApp() {

const introScreen =
    document.getElementById(
        'intro-screen'
    );


const mainApp =
    document.getElementById(
        'main-app'
    );


const navUserName =
    document.getElementById(
        'nav-user-name'
    );


if (introScreen) {

    introScreen.classList.add(
        'hidden'
    );

}


if (mainApp) {

    mainApp.classList.remove(
        'hidden'
    );


    setTimeout(() => {

        mainApp.classList.remove(
            'opacity-0'
        );

    }, 50);

}


if (
    navUserName &&
    currentUser
) {

    navUserName.textContent =
        currentUser.name
            .split(' ')[0];

}


updateUserReplyNotification();

updateAllNotificationBadges();

}

function logoutUser() {

localStorage.removeItem(
    'app_current_user'
);


currentUser = null;


location.reload();

}

/* =========================================================
7. NAVIGATION
========================================================= */

function showSection(sectionId) {

const sections =
    document.querySelectorAll(
        '.app-section'
    );


sections.forEach(section => {

    section.classList.add(
        'hidden'
    );

});


const target =
    document.getElementById(
        sectionId
    );


if (target) {

    target.classList.remove(
        'hidden'
    );


    window.scrollTo({

        top: 0,

        behavior:
            'smooth'

    });

}

}

/*
فتح قسم المحتوى
وإزالة إشعار المحتوى الجديد
*/

function openContentSection(sectionId) {

showSection(sectionId);

markSectionAsSeen(sectionId);

}

/* =========================================================
8. THEME
========================================================= */

function toggleTheme() {

isDarkMode =
    !isDarkMode;


const body =
    document.getElementById(
        'app-body'
    );


const themeBtnText =
    document.getElementById(
        'theme-btn-text'
    );


if (!body) return;


if (isDarkMode) {

    body.className =
        'theme-dark bg-slate-950 text-slate-100 min-h-screen font-cairo text-xs sm:text-sm selection:bg-amber-400 selection:text-black overflow-x-hidden';


    if (themeBtnText) {

        themeBtnText.textContent =
            '🌙 الداكن';

    }

}


else {

    body.className =
        'theme-light bg-slate-100 text-slate-900 min-h-screen font-cairo text-xs sm:text-sm selection:bg-amber-400 selection:text-black overflow-x-hidden';


    if (themeBtnText) {

        themeBtnText.textContent =
            '☀️ المضيء';

    }

}

}

/* =========================================================
9. USER ACCOUNT
========================================================= */

function openUserAccountModal() {

if (!currentUser) return;


const modal =
    document.getElementById(
        'user-account-modal'
    );


const userInfoCard =
    document.getElementById(
        'user-info-card'
    );


const replyBox =
    document.getElementById(
        'user-reply-box'
    );


const latestUserData =
    usersList.find(
        user =>
            user.phone ===
            currentUser.phone
    );


if (latestUserData) {

    currentUser =
        latestUserData;


    localStorage.setItem(
        'app_current_user',
        JSON.stringify(currentUser)
    );

}


if (userInfoCard) {

    userInfoCard.innerHTML = `

        <p>
            <strong>
                الاسم:
            </strong>

            ${escapeHtml(currentUser.name)}
        </p>

        <p>
            <strong>
                الهاتف:
            </strong>

            <span dir="ltr">
                ${escapeHtml(currentUser.phone)}
            </span>
        </p>

        <p>
            <strong>
                الصف:
            </strong>

            ${escapeHtml(currentUser.grade)}
        </p>

        <p>
            <strong>
                المدرسة/السنتر:
            </strong>

            ${escapeHtml(currentUser.school)}
        </p>

    `;

}


if (replyBox) {

    replyBox.textContent =
        latestUserData &&
        latestUserData.reply

            ? latestUserData.reply

            : 'لا يوجد رد بعد من إدارة المنصة.';

}


if (modal) {

    modal.classList.remove(
        'hidden'
    );

}


markReplyAsSeen();

}

function closeUserAccountModal() {

const modal =
    document.getElementById(
        'user-account-modal'
    );


if (modal) {

    modal.classList.add(
        'hidden'
    );

}

}

function sendStudentMessage(event) {

event.preventDefault();


const input =
    document.getElementById(
        'student-msg-text'
    );


if (!input) return;


const msgText =
    input.value.trim();


if (!msgText) return;


if (!currentUser) {

    alert(
        'يرجى تسجيل الدخول أولاً لإرسال رسالة.'
    );

    return;

}


currentUser.message =
    msgText;


const index =
    usersList.findIndex(
        user =>
            user.phone ===
            currentUser.phone
    );


if (index !== -1) {

    usersList[index].message =
        msgText;


    saveUsers();


    localStorage.setItem(
        'app_current_user',
        JSON.stringify(currentUser)
    );

}


triggerVibration();


alert(
    'تم إرسال رسالتك بنجاح إلى المستر.'
);


input.value = '';

}

/* =========================================================
10. USER REPLY NOTIFICATIONS
========================================================= */

function updateUserReplyNotification() {

if (!currentUser) return;


const latestUserData =
    usersList.find(
        user =>
            user.phone ===
            currentUser.phone
    );


const replySeen =
    localStorage.getItem(
        `reply_seen_${currentUser.phone}`
    );


const hasNewReply =
    latestUserData &&
    latestUserData.reply &&
    replySeen !== latestUserData.reply;


document
    .querySelectorAll(
        '#badge-user-nav, #badge-user-mobile'
    )
    .forEach(badge => {

        if (hasNewReply) {

            badge.classList.remove(
                'hidden'
            );

        }

        else {

            badge.classList.add(
                'hidden'
            );

        }

    });

}

function markReplyAsSeen() {

if (!currentUser) return;


const latestUserData =
    usersList.find(
        user =>
            user.phone ===
            currentUser.phone
    );


if (
    latestUserData &&
    latestUserData.reply
) {

    localStorage.setItem(
        `reply_seen_${currentUser.phone}`,
        latestUserData.reply
    );

}


updateUserReplyNotification();

}

/* =========================================================
11. VIBRATION
========================================================= */

function triggerVibration() {

if ('vibrate' in navigator) {

    navigator.vibrate(
        [100, 60, 100]
    );

}

}

/* =========================================================
12. NEW CONTENT NOTIFICATIONS
========================================================= */

function getSectionSeenKey(section) {

return `section_seen_${section}`;

}

function getLatestSectionContent(section) {

return appContents
    .filter(
        item =>
            item.section === section
    )
    .sort(
        (a, b) =>
            b.id - a.id
    )[0];

}

function markSectionAsSeen(section) {

const latest =
    getLatestSectionContent(
        section
    );


if (!latest) return;


localStorage.setItem(
    getSectionSeenKey(section),
    String(latest.id)
);


updateAllNotificationBadges();

}

function updateAllNotificationBadges() {

const sections = [

    'news',

    'courses',

    'pdfs',

    'quizzes'

];


sections.forEach(section => {

    const latest =
        getLatestSectionContent(
            section
        );


    const seenId =
        localStorage.getItem(
            getSectionSeenKey(section)
        );


    const hasNewContent =
        latest &&
        String(latest.id) !==
        String(seenId);


    document
        .querySelectorAll(
            `#badge-${section}-nav, #badge-${section}-mobile`
        )
        .forEach(badge => {

            if (hasNewContent) {

                badge.classList.remove(
                    'hidden'
                );

            }

            else {

                badge.classList.add(
                    'hidden'
                );

            }

        });

});

}

/* =========================================================
13. CONTENT RENDERING
========================================================= */

function renderAllContents(
filterQuery = ''
) {

const containers = {

    news:
        document.getElementById(
            'news-container'
        ),

    courses:
        document.getElementById(
            'courses-container'
        ),

    pdfs:
        document.getElementById(
            'pdfs-container'
        ),

    quizzes:
        document.getElementById(
            'quizzes-container'
        )

};


Object.values(containers)
    .forEach(container => {

        if (container) {

            container.innerHTML = '';

        }

    });


const query =
    filterQuery
        .toLowerCase()
        .trim();


const filtered =
    appContents.filter(item => {

        const title =
            String(
                item.title || ''
            ).toLowerCase();


        return title.includes(
            query
        );

    });


filtered.forEach(item => {

    const targetContainer =
        containers[item.section];


    if (!targetContainer) return;


    if (
        item.section === 'quizzes'
    ) {

        renderQuizCard(
            item,
            targetContainer
        );

    }

    else {

        renderNormalContentCard(
            item,
            targetContainer
        );

    }

});


renderEmptyContainers(
    containers
);

}

/* =========================================================
14. NORMAL CONTENT CARD
========================================================= */

function renderNormalContentCard(
item,
targetContainer
) {

const card =
    document.createElement(
        'div'
    );


card.className =
    'content-card bg-slate-900/90 border border-slate-800 p-4 rounded-xl shadow-md space-y-2 relative';


let mediaHtml = '';


if (item.fileData) {

    if (
        item.fileType &&
        item.fileType.startsWith(
            'image/'
        )
    ) {

        mediaHtml = `

            <img
                src="${item.fileData}"
                class="w-full max-h-80 object-cover rounded-lg my-2"
                alt="مرفق">

        `;

    }


    else if (

        item.fileType &&
        item.fileType.startsWith(
            'video/'
        )

    ) {

        mediaHtml = `

            <video
                src="${item.fileData}"
                controls
                class="w-full max-h-80 rounded-lg my-2">
            </video>

        `;

    }


    else if (

        item.fileType ===
        'application/pdf'

    ) {

        mediaHtml = `

            <a
                href="${item.fileData}"
                download="ملف.pdf"
                class="inline-block my-2 text-amber-400 underline font-bold">

                📄 تحميل ملف PDF

            </a>

        `;

    }

}


let linkHtml = '';


if (item.link) {

    linkHtml = `

        <a
            href="${escapeAttribute(item.link)}"
            target="_blank"
            rel="noopener noreferrer"
            class="inline-block mt-1 text-xs text-amber-400 font-bold hover:underline">

            🔗 فتح الرابط الخارجي

        </a>

    `;

}


card.innerHTML = `

    <div class="flex justify-between items-start gap-3">

        <h4 class="font-bold text-amber-300 text-sm md:text-base">

            ${escapeHtml(item.title)}

        </h4>


        <div class="flex items-center gap-2 shrink-0">

            <span class="text-[10px] text-slate-500">

                ${escapeHtml(item.date || '')}

            </span>


            <button
                onclick="deleteContent(${item.id})"
                class="text-red-400 hover:text-red-300 font-bold text-xs bg-red-500/10 p-1.5 rounded border border-red-500/20"
                title="حذف المحتوى">

                🗑️

            </button>

        </div>

    </div>


    ${mediaHtml}


    ${linkHtml}

`;


targetContainer.appendChild(
    card
);

}

/* =========================================================
15. QUIZ CARD
========================================================= */

function renderQuizCard(
quiz,
targetContainer
) {

const card =
    document.createElement(
        'div'
    );


card.className =
    'quiz-card bg-slate-900 border border-slate-800 p-5 rounded-xl shadow-md space-y-3';


const questionsCount =
    Array.isArray(
        quiz.questions
    )

        ? quiz.questions.length

        : 0;


card.innerHTML = `

    <div class="flex justify-between gap-3 items-start">

        <div>

            <h4 class="font-black text-amber-400 text-base">

                📝
                ${escapeHtml(quiz.title)}

            </h4>


            <p class="text-slate-400 text-xs mt-2">

                عدد الأسئلة:
                ${questionsCount}

                <span class="mx-1">
                    |
                </span>

                ⏱️
                ${quiz.time || 15}
                دقيقة

            </p>

        </div>


        <button
            onclick="deleteContent(${quiz.id})"
            class="text-red-400 bg-red-500/10 border border-red-500/20 rounded-lg p-1.5 text-xs">

            🗑️

        </button>

    </div>


    <button
        onclick="startQuiz(${quiz.id})"
        class="w-full py-3 bg-amber-400 text-slate-950 font-black rounded-xl hover:bg-amber-300 transition">

        🚀 بدء الاختبار

    </button>

`;


targetContainer.appendChild(
    card
);

}

/* =========================================================
16. EMPTY CONTAINERS
========================================================= */

function renderEmptyContainers(
containers
) {

Object.entries(containers)
    .forEach(
        ([section, container]) => {

            if (
                !container ||
                container.children.length > 0
            ) {

                return;

            }


            let text =
                'لا يوجد محتوى حالياً.';


            if (
                section === 'quizzes'
            ) {

                text =
                    'لا توجد اختبارات منشورة حالياً.';

            }


            container.innerHTML = `

                <div class="text-center py-10 text-slate-500 border border-dashed border-slate-700 rounded-xl">

                    ${text}

                </div>

            `;

        }
    );

}

/* =========================================================
17. SEARCH
========================================================= */

function handleSearch() {

const input =
    document.getElementById(
        'search-input'
    );


if (!input) return;


renderAllContents(
    input.value
);

}

/* =========================================================
18. DELETE CONTENT
========================================================= */

function deleteContent(id) {

const adminPass =
    localStorage.getItem(
        'app_admin_pass'
    ) ||
    ADMIN_PASSWORD_DEFAULT;


const inputPass =
    prompt(
        'أدخل كلمة مرور الأدمن لتأكيد حذف المحتوى:'
    );


if (
    inputPass === null
) {

    return;

}


if (
    inputPass !== adminPass
) {

    alert(
        'كلمة المرور غير صحيحة.'
    );

    return;

}


const target =
    appContents.find(
        item =>
            Number(item.id) ===
            Number(id)
    );


if (!target) {

    alert(
        'لم يتم العثور على المحتوى.'
    );

    return;

}


const confirmed =
    confirm(
        `هل تريد حذف "${target.title}"؟`
    );


if (!confirmed) return;


appContents =
    appContents.filter(
        item =>
            Number(item.id) !==
            Number(id)
    );


saveContents();


renderAllContents();


updateAllNotificationBadges();


alert(
    'تم حذف المحتوى بنجاح.'
);

}

/* =========================================================
19. ADMIN MODAL
========================================================= */

function openAdminModal() {

const modal =
    document.getElementById(
        'admin-modal'
    );


if (!modal) return;


modal.classList.remove(
    'hidden'
);

}

function closeAdminModal() {

const modal =
    document.getElementById(
        'admin-modal'
    );


if (modal) {

    modal.classList.add(
        'hidden'
    );

}


const auth =
    document.getElementById(
        'admin-auth'
    );


const dashboard =
    document.getElementById(
        'admin-dashboard-content'
    );


if (auth) {

    auth.classList.remove(
        'hidden'
    );

}


if (dashboard) {

    dashboard.classList.add(
        'hidden'
    );

}

}

function verifyAdminPass() {

const input =
    document.getElementById(
        'admin-pass-input'
    );


if (!input) return;


const passInput =
    input.value;


const adminPass =
    localStorage.getItem(
        'app_admin_pass'
    ) ||
    ADMIN_PASSWORD_DEFAULT;


if (
    passInput !== adminPass
) {

    alert(
        'كلمة المرور غير صحيحة.'
    );

    return;

}


openAdminDashboard();

}

function openAdminDashboard() {

const auth =
    document.getElementById(
        'admin-auth'
    );


const dashboard =
    document.getElementById(
        'admin-dashboard-content'
    );


if (auth) {

    auth.classList.add(
        'hidden'
    );

}


if (dashboard) {

    dashboard.classList.remove(
        'hidden'
    );

}


renderAdminTable();

}

/* =========================================================
20. ADMIN TABLE
========================================================= */

function renderAdminTable() {

const tbody =
    document.getElementById(
        'admin-table-body'
    );


if (!tbody) return;


tbody.innerHTML = '';


usersList.forEach(
    (user, index) => {

        const tr =
            document.createElement(
                'tr'
            );


        tr.className =
            'hover:bg-slate-800/50 transition';


        tr.innerHTML = `

            <td class="p-2.5 font-bold">

                ${escapeHtml(user.name)}

            </td>


            <td class="p-2.5">

                ${escapeHtml(user.grade)}

            </td>


            <td
                class="p-2.5"
                dir="ltr">

                ${escapeHtml(user.phone)}

            </td>


            <td class="p-2.5 italic text-slate-300 max-w-[250px] break-words">

                ${escapeHtml(
                    user.message ||
                    'لا توجد رسالة'
                )}

            </td>


            <td class="p-2.5 text-amber-300 max-w-[250px] break-words">

                ${escapeHtml(
                    user.reply ||
                    'لم يتم الرد'
                )}

            </td>


            <td class="p-2.5 text-center">

                <div class="flex justify-center gap-1">

                    <button
                        onclick="replyToStudent(${index})"
                        class="px-2 py-1 bg-amber-400/20 text-amber-300 border border-amber-400/30 rounded-lg text-[11px] font-bold">

                        الرد

                    </button>


                    <button
                        onclick="deleteStudent(${index})"
                        class="px-2 py-1 bg-red-500/20 text-red-400 border border-red-500/30 rounded-lg text-[11px] font-bold">

                        حذف

                    </button>

                </div>

            </td>

        `;


        tbody.appendChild(
            tr
        );

    }
);

}

/* =========================================================
21. REPLY TO STUDENT
========================================================= */

function replyToStudent(index) {

const user =
    usersList[index];


if (!user) return;


const replyMsg =
    prompt(
        `اكتب ردك للطالب: ${user.name}`,
        user.reply || ''
    );


if (
    replyMsg === null
) {

    return;

}


usersList[index].reply =
    replyMsg.trim();


saveUsers();


renderAdminTable();


if (

    currentUser &&
    currentUser.phone ===
    usersList[index].phone

) {

    currentUser.reply =
        usersList[index].reply;


    localStorage.setItem(
        'app_current_user',
        JSON.stringify(currentUser)
    );

}


updateUserReplyNotification();


triggerVibration();

}

/* =========================================================
22. DELETE STUDENT
========================================================= */

function deleteStudent(index) {

const user =
    usersList[index];


if (!user) return;


const confirmed =
    confirm(
        `هل أنت متأكد من إزالة ${user.name} من المنصة؟`
    );


if (!confirmed) return;


const deletedPhone =
    user.phone;


usersList.splice(
    index,
    1
);


saveUsers();


renderAdminTable();


if (

    currentUser &&
    currentUser.phone ===
    deletedPhone

) {

    logoutUser();

}

}

/* =========================================================
23. ADMIN PUBLISH MODE
========================================================= */

function toggleAdminPublishMode() {

const target =
    document.getElementById(
        'admin-target-section'
    );


const normalForm =
    document.getElementById(
        'normal-content-form'
    );


const quizForm =
    document.getElementById(
        'quiz-publish-form'
    );


if (
    !target ||
    !normalForm ||
    !quizForm
) {

    return;

}


if (
    target.value ===
    'quizzes'
) {

    normalForm.classList.add(
        'hidden'
    );


    quizForm.classList.remove(
        'hidden'
    );


    if (
        adminQuestionCount === 0
    ) {

        addQuizQuestion();

    }

}


else {

    quizForm.classList.add(
        'hidden'
    );


    normalForm.classList.remove(
        'hidden'
    );

}

}

/* =========================================================
24. PUBLISH NORMAL CONTENT
========================================================= */

function publishNews() {

const target =
    document.getElementById(
        'admin-target-section'
    );


if (
    target &&
    target.value ===
    'quizzes'
) {

    alert(
        'أنت في وضع نشر الاختبارات.'
    );

    return;

}


const titleInput =
    document.getElementById(
        'admin-news-input'
    );


const linkInput =
    document.getElementById(
        'admin-news-link'
    );


const fileInput =
    document.getElementById(
        'admin-news-file'
    );


if (
    !target ||
    !titleInput ||
    !linkInput ||
    !fileInput
) {

    return;

}


const title =
    titleInput.value.trim();


const link =
    linkInput.value.trim();


if (!title) {

    alert(
        'يرجى إدخال عنوان أو نص المحتوى.'
    );

    return;

}


const newContent = {

    id:
        Date.now(),

    section:
        target.value,

    title,

    link,

    fileData:
        '',

    fileType:
        '',

    date:
        new Date()
            .toLocaleDateString(
                'ar-EG'
            )

};


const file =
    fileInput.files[0];


if (file) {

    const reader =
        new FileReader();


    reader.onload =
        function(event) {

            newContent.fileData =
                event.target.result;


            newContent.fileType =
                file.type;


            saveAndRenderPublishedContent(
                newContent
            );

        };


    reader.onerror =
        function() {

            alert(
                'حدث خطأ أثناء قراءة الملف.'
            );

        };


    reader.readAsDataURL(
        file
    );

}


else {

    saveAndRenderPublishedContent(
        newContent
    );

}

}

function saveAndRenderPublishedContent(
content
) {

appContents.unshift(
    content
);


saveContents();


const titleInput =
    document.getElementById(
        'admin-news-input'
    );


const linkInput =
    document.getElementById(
        'admin-news-link'
    );


const fileInput =
    document.getElementById(
        'admin-news-file'
    );


if (titleInput) {

    titleInput.value = '';

}


if (linkInput) {

    linkInput.value = '';

}


if (fileInput) {

    fileInput.value = '';

}


renderAllContents();


updateAllNotificationBadges();


triggerVibration();


alert(
    'تم نشر المحتوى بنجاح.'
);

}

/* =========================================================
25. ADD QUIZ QUESTION
========================================================= */

function addQuizQuestion() {

const container =
    document.getElementById(
        'admin-questions-container'
    );


if (!container) return;


adminQuestionCount++;


const questionNumber =
    adminQuestionCount;


const questionCard =
    document.createElement(
        'div'
    );


questionCard.className =
    'admin-question-card space-y-3';


questionCard.dataset.questionId =
    questionNumber;


questionCard.innerHTML = `

    <div class="flex justify-between items-center gap-2">

        <h5 class="font-black text-amber-400">

            السؤال رقم
            ${questionNumber}

        </h5>


        <button
            type="button"
            onclick="removeQuizQuestion(this)"
            class="text-red-400 text-xs bg-red-500/10 px-2 py-1 rounded-lg">

            حذف السؤال

        </button>

    </div>


    <input
        type="text"
        class="quiz-question-text w-full p-3 bg-slate-800 border border-slate-700 rounded-xl"
        placeholder="اكتب السؤال هنا">


    <div class="grid grid-cols-1 sm:grid-cols-2 gap-2">


        <input
            type="text"
            class="quiz-option-input w-full p-3 bg-slate-800 border border-slate-700 rounded-xl"
            placeholder="الإجابة الأولى">


        <input
            type="text"
            class="quiz-option-input w-full p-3 bg-slate-800 border border-slate-700 rounded-xl"
            placeholder="الإجابة الثانية">


        <input
            type="text"
            class="quiz-option-input w-full p-3 bg-slate-800 border border-slate-700 rounded-xl"
            placeholder="الإجابة الثالثة">


        <input
            type="text"
            class="quiz-option-input w-full p-3 bg-slate-800 border border-slate-700 rounded-xl"
            placeholder="الإجابة الرابعة">

    </div>


    <div>

        <label class="block text-slate-300 mb-1">

            اختر الإجابة الصحيحة

        </label>


        <select
            class="quiz-correct-answer w-full p-3 bg-slate-800 border border-slate-700 rounded-xl">

            <option value="">
                اختر الإجابة الصحيحة
            </option>

            <option value="0">
                الإجابة الأولى
            </option>

            <option value="1">
                الإجابة الثانية
            </option>

            <option value="2">
                الإجابة الثالثة
            </option>

            <option value="3">
                الإجابة الرابعة
            </option>

        </select>

    </div>

`;


container.appendChild(
    questionCard
);

}

/* =========================================================
26. REMOVE QUIZ QUESTION
========================================================= */

function removeQuizQuestion(button) {

const card =
    button.closest(
        '.admin-question-card'
    );


if (card) {

    card.remove();

    updateQuestionNumbers();

}

}

function updateQuestionNumbers() {

const cards =
    document.querySelectorAll(
        '#admin-questions-container .admin-question-card'
    );


cards.forEach(
    (card, index) => {

        const title =
            card.querySelector(
                'h5'
            );


        if (title) {

            title.textContent =
                `السؤال رقم ${index + 1}`;

        }

    }
);


adminQuestionCount =
    cards.length;

}

/* =========================================================
27. PUBLISH QUIZ
========================================================= */

function publishQuiz() {

const titleInput =
    document.getElementById(
        'quiz-admin-title'
    );


const timeInput =
    document.getElementById(
        'quiz-admin-time'
    );


const questionCards =
    document.querySelectorAll(
        '#admin-questions-container .admin-question-card'
    );


if (
    !titleInput ||
    !timeInput
) {

    return;

}


const title =
    titleInput.value.trim();


const time =
    Number(
        timeInput.value
    );


if (!title) {

    alert(
        'يرجى كتابة عنوان الاختبار.'
    );

    return;

}


if (
    !time ||
    time < 1
) {

    alert(
        'يرجى تحديد مدة صحيحة للاختبار.'
    );

    return;

}


if (
    questionCards.length === 0
) {

    alert(
        'يرجى إضافة سؤال واحد على الأقل.'
    );

    return;

}


const questions = [];


for (
    let i = 0;
    i < questionCards.length;
    i++
) {

    const card =
        questionCards[i];


    const questionInput =
        card.querySelector(
            '.quiz-question-text'
        );


    const optionInputs =
        card.querySelectorAll(
            '.quiz-option-input'
        );


    const correctSelect =
        card.querySelector(
            '.quiz-correct-answer'
        );


    const questionText =
        questionInput
            .value
            .trim();


    const options =
        Array.from(
            optionInputs
        ).map(
            input =>
                input.value.trim()
        );


    const correctAnswer =
        correctSelect.value;


    if (!questionText) {

        alert(
            `يرجى كتابة نص السؤال رقم ${i + 1}.`
        );

        return;

    }


    if (
        options.some(
            option =>
                !option
        )
    ) {

        alert(
            `يرجى كتابة جميع إجابات السؤال رقم ${i + 1}.`
        );

        return;

    }


    if (
        correctAnswer === ''
    ) {

        alert(
            `يرجى تحديد الإجابة الصحيحة للسؤال رقم ${i + 1}.`
        );

        return;

    }


    questions.push({

        question:
            questionText,

        options,

        correctAnswer:
            Number(
                correctAnswer
            )

    });

}


const quiz = {

    id:
        Date.now(),

    section:
        'quizzes',

    title,

    time,

    questions,

    date:
        new Date()
            .toLocaleDateString(
                'ar-EG'
            )

};


appContents.unshift(
    quiz
);


saveContents();


resetQuizPublishingForm();


renderAllContents();


updateAllNotificationBadges();


triggerVibration();


alert(
    'تم نشر الاختبار بنجاح.'
);

}

/* =========================================================
28. RESET QUIZ FORM
========================================================= */

function resetQuizPublishingForm() {

const titleInput =
    document.getElementById(
        'quiz-admin-title'
    );


const timeInput =
    document.getElementById(
        'quiz-admin-time'
    );


const container =
    document.getElementById(
        'admin-questions-container'
    );


if (titleInput) {

    titleInput.value = '';

}


if (timeInput) {

    timeInput.value = 15;

}


if (container) {

    container.innerHTML = '';

}


adminQuestionCount = 0;


addQuizQuestion();

}

/* =========================================================
29. START QUIZ
========================================================= */

function startQuiz(quizId) {

const quiz =
    appContents.find(
        item =>

            Number(item.id) ===
            Number(quizId) &&

            item.section ===
            'quizzes'
    );


if (!quiz) {

    alert(
        'الاختبار غير موجود.'
    );

    return;

}


if (

    !Array.isArray(
        quiz.questions
    ) ||

    quiz.questions.length === 0

) {

    alert(
        'هذا الاختبار لا يحتوي على أسئلة.'
    );

    return;

}


currentQuiz =
    quiz;


const modal =
    document.getElementById(
        'quiz-modal'
    );


const title =
    document.getElementById(
        'quiz-title'
    );


const questionsContainer =
    document.getElementById(
        'quiz-questions-container'
    );


const form =
    document.getElementById(
        'quiz-form'
    );


const result =
    document.getElementById(
        'quiz-result'
    );


if (

    !modal ||
    !title ||
    !questionsContainer

) {

    return;

}


title.textContent =
    quiz.title;


questionsContainer.innerHTML = '';


quiz.questions.forEach(
    (question, questionIndex) => {

        const questionBox =
            document.createElement(
                'div'
            );


        questionBox.className =
            'quiz-question bg-slate-950 border border-slate-800 rounded-xl p-4 space-y-3';


        let optionsHtml = '';


        question.options.forEach(
            (option, optionIndex) => {

                optionsHtml += `

                    <label class="quiz-option">

                        <input
                            type="radio"
                            name="question_${questionIndex}"
                            value="${optionIndex}">

                        <span>

                            ${escapeHtml(option)}

                        </span>

                    </label>

                `;

            }
        );


        questionBox.innerHTML = `

            <h4 class="font-bold text-sm text-slate-100">

                ${questionIndex + 1}.
                ${escapeHtml(question.question)}

            </h4>


            <div class="space-y-2">

                ${optionsHtml}

            </div>

        `;


        questionsContainer.appendChild(
            questionBox
        );

    }
);


if (form) {

    form.classList.remove(
        'hidden'
    );

}


if (result) {

    result.classList.add(
        'hidden'
    );

}


modal.classList.remove(
    'hidden'
);


document.body.style.overflow =
    'hidden';


startQuizTimer(
    Number(quiz.time) || 15
);

}

/* =========================================================
30. QUIZ TIMER
========================================================= */

function startQuizTimer(minutes) {

clearQuizTimer();


quizRemainingSeconds =
    Math.max(
        1,
        Math.floor(minutes * 60)
    );


updateQuizTimerDisplay();


quizTimerInterval =
    setInterval(() => {

        quizRemainingSeconds--;


        updateQuizTimerDisplay();


        if (

            quizRemainingSeconds <= 0

        ) {

            clearQuizTimer();


            alert(
                'انتهى وقت الاختبار.'
            );


            submitQuizAutomatically();

        }

    }, 1000);

}

function updateQuizTimerDisplay() {

const timer =
    document.getElementById(
        'quiz-timer'
    );


const timerBox =
    document.getElementById(
        'quiz-timer-box'
    );


if (!timer) return;


const minutes =
    Math.floor(
        quizRemainingSeconds / 60
    );


const seconds =
    quizRemainingSeconds % 60;


timer.textContent =

    `${String(minutes).padStart(2, '0')}:${String(seconds).padStart(2, '0')}`;


if (
    timerBox
) {

    if (

        quizRemainingSeconds <= 60

    ) {

        timerBox.classList.add(
            'quiz-time-warning'
        );

    }

    else {

        timerBox.classList.remove(
            'quiz-time-warning'
        );

    }

}

}

function clearQuizTimer() {

if (
    quizTimerInterval
) {

    clearInterval(
        quizTimerInterval
    );


    quizTimerInterval =
        null;

}

}

/* =========================================================
31. SUBMIT QUIZ
========================================================= */

function submitQuiz(event) {

if (event) {

    event.preventDefault();

}


calculateQuizResult();

}

function submitQuizAutomatically() {

calculateQuizResult();

}

function calculateQuizResult() {

if (
    !currentQuiz
) {

    return;

}


clearQuizTimer();


let score = 0;


const total =
    currentQuiz.questions.length;


currentQuiz.questions.forEach(
    (question, index) => {

        const selected =
            document.querySelector(
                `input[name="question_${index}"]:checked`
            );


        if (

            selected &&
            Number(
                selected.value
            ) ===
            Number(
                question.correctAnswer
            )

        ) {

            score++;

        }

    }
);


const percentage =
    Math.round(
        (score / total) * 100
    );


showQuizResult(
    score,
    total,
    percentage
);

}

/* =========================================================
32. SHOW QUIZ RESULT
========================================================= */

function showQuizResult(
score,
total,
percentage
) {

const form =
    document.getElementById(
        'quiz-form'
    );


const result =
    document.getElementById(
        'quiz-result'
    );


const scoreBox =
    document.getElementById(
        'quiz-score'
    );


const resultText =
    document.getElementById(
        'quiz-result-text'
    );


if (form) {

    form.classList.add(
        'hidden'
    );

}


if (result) {

    result.classList.remove(
        'hidden'
    );

}


if (scoreBox) {

    scoreBox.textContent =
        `${score} / ${total}`;

}


if (resultText) {

    let message = '';


    if (
        percentage === 100
    ) {

        message =
            'ممتاز! إجابة كاملة 🎉';

    }

    else if (
        percentage >= 80
    ) {

        message =
            'أداء رائع جداً، استمر في التميز 👏';

    }

    else if (
        percentage >= 60
    ) {

        message =
            'نتيجة جيدة، يمكنك الوصول للأفضل 💪';

    }

    else {

        message =
            'لا بأس، راجع الدرس وحاول مرة أخرى 📚';

    }


    resultText.textContent =
        `النتيجة: ${percentage}% — ${message}`;

}


triggerVibration();

}

/* =========================================================
33. CLOSE QUIZ MODAL
========================================================= */

function closeQuizModal() {

clearQuizTimer();


const modal =
    document.getElementById(
        'quiz-modal'
    );


if (modal) {

    modal.classList.add(
        'hidden'
    );

}


document.body.style.overflow =
    '';


currentQuiz = null;

}

/* =========================================================
34. ESCAPE HTML
========================================================= */

function escapeHtml(value) {

if (
    value === null ||
    value === undefined
) {

    return '';

}


return String(value)

    .replace(
        /&/g,
        '&amp;'
    )

    .replace(
        /</g,
        '&lt;'
    )

    .replace(
        />/g,
        '&gt;'
    )

    .replace(
        /"/g,
        '&quot;'
    )

    .replace(
        /'/g,
        '&#039;'
    );

}

function escapeAttribute(value) {

return escapeHtml(value);

}

/* =========================================================
35. CLOSE MODALS WITH ESC
========================================================= */

document.addEventListener(
'keydown',
event => {

    if (
        event.key === 'Escape'
    ) {

        closeQuizModal();

    }

}

);
