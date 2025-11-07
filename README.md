<!doctype html>
<html lang="en">
 <head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>BANTAY LAHI - Indigenous Community Information System</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <script src="/_sdk/data_sdk.js"></script>
  <script src="/_sdk/element_sdk.js"></script>
  <style>
    body {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
    }
    
    * {
      box-sizing: border-box;
    }

    html, body {
      height: 100%;
    }

    .logo-container {
      position: relative;
      display: inline-block;
    }

    .stat-card {
      transition: transform 0.2s, box-shadow 0.2s;
    }

    .stat-card:hover {
      transform: translateY(-2px);
      box-shadow: 0 8px 16px rgba(0, 0, 0, 0.1);
    }

    .nav-item {
      transition: all 0.2s;
    }

    .nav-item:hover {
      background-color: rgba(255, 255, 255, 0.1);
    }

    .nav-item.active {
      background-color: rgba(255, 255, 255, 0.2);
      border-left: 4px solid white;
    }

    .form-input {
      transition: border-color 0.2s, box-shadow 0.2s;
    }

    .form-input:focus {
      outline: none;
      border-color: #3b82f6;
      box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.1);
    }

    .btn {
      transition: all 0.2s;
    }

    .btn:hover:not(:disabled) {
      transform: translateY(-1px);
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.15);
    }

    .btn:active:not(:disabled) {
      transform: translateY(0);
    }

    .btn:disabled {
      opacity: 0.6;
      cursor: not-allowed;
    }

    .table-row {
      transition: background-color 0.15s;
    }

    .table-row:hover {
      background-color: rgba(59, 130, 246, 0.05);
    }

    .loading-spinner {
      border: 3px solid rgba(255, 255, 255, 0.3);
      border-top-color: white;
      border-radius: 50%;
      width: 24px;
      height: 24px;
      animation: spin 0.8s linear infinite;
    }

    @keyframes spin {
      to { transform: rotate(360deg); }
    }

    .toast {
      position: fixed;
      bottom: 24px;
      right: 24px;
      padding: 16px 24px;
      border-radius: 8px;
      color: white;
      font-weight: 500;
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
      animation: slideIn 0.3s ease-out;
      z-index: 1000;
    }

    @keyframes slideIn {
      from {
        transform: translateX(400px);
        opacity: 0;
      }
      to {
        transform: translateX(0);
        opacity: 1;
      }
    }

    .modal-backdrop {
      background-color: rgba(0, 0, 0, 0.5);
      animation: fadeIn 0.2s ease-out;
    }

    @keyframes fadeIn {
      from { opacity: 0; }
      to { opacity: 1; }
    }

    .modal-content {
      animation: slideUp 0.3s ease-out;
    }

    @keyframes slideUp {
      from {
        transform: translateY(50px);
        opacity: 0;
      }
      to {
        transform: translateY(0);
        opacity: 1;
      }
    }

    .barangay-card {
      cursor: pointer;
      transition: all 0.2s;
    }

    .barangay-card:hover {
      transform: translateY(-2px);
      box-shadow: 0 6px 12px rgba(0, 0, 0, 0.1);
    }

    .photo-preview {
      width: 150px;
      height: 150px;
      object-fit: cover;
      border-radius: 8px;
    }

    .camera-container {
      position: relative;
      width: 100%;
      max-width: 400px;
    }

    video {
      width: 100%;
      border-radius: 8px;
    }

    .tree-node {
      position: relative;
      padding: 10px;
      border: 2px solid #3b82f6;
      border-radius: 8px;
      background: white;
      margin: 10px;
      display: inline-block;
    }

    .tree-line {
      position: absolute;
      background: #3b82f6;
    }
  </style>
  <style>@view-transition { navigation: auto; }</style>
 </head>
 <body>
  <div id="app" class="h-full"><!-- Login Screen -->
   <div id="loginScreen" class="flex items-center justify-center min-h-full p-4">
    <div class="w-full max-w-md">
     <div class="text-center mb-8"><!-- Logo SVG -->
      <div class="logo-container mx-auto mb-4">
       <svg width="120" height="120" viewbox="0 0 120 120" xmlns="http://www.w3.org/2000/svg"><!-- Shield Background --> <path d="M60 10 L100 30 L100 70 Q100 90 60 110 Q20 90 20 70 L20 30 Z" fill="#059669" stroke="#047857" stroke-width="2" /> <!-- Mountain/Tribal Pattern --> <path d="M40 50 L50 35 L60 50 L70 35 L80 50" fill="none" stroke="#fbbf24" stroke-width="3" stroke-linecap="round" /> <!-- People Silhouettes --> <circle cx="45" cy="65" r="5" fill="#fbbf24" /> <path d="M45 70 L45 80 M40 75 L50 75" stroke="#fbbf24" stroke-width="2" stroke-linecap="round" /> <circle cx="60" cy="65" r="5" fill="#fbbf24" /> <path d="M60 70 L60 80 M55 75 L65 75" stroke="#fbbf24" stroke-width="2" stroke-linecap="round" /> <circle cx="75" cy="65" r="5" fill="#fbbf24" /> <path d="M75 70 L75 80 M70 75 L80 75" stroke="#fbbf24" stroke-width="2" stroke-linecap="round" /> <!-- Decorative Elements --> <circle cx="30" cy="40" r="3" fill="#fbbf24" opacity="0.6" /> <circle cx="90" cy="40" r="3" fill="#fbbf24" opacity="0.6" /> <circle cx="60" cy="95" r="3" fill="#fbbf24" opacity="0.6" />
       </svg>
      </div>
      <h1 id="loginSystemTitle" class="text-4xl font-bold mb-2" style="color: #059669;">BANTAY LAHI</h1>
      <p id="loginSystemSubtitle" class="text-lg opacity-75">Indigenous Community Information System</p>
      <p id="loginLocationLabel" class="text-sm opacity-60 mt-1">Catanauan, Quezon</p>
     </div>
     <div class="bg-white rounded-xl shadow-lg p-8">
      <div class="flex border-b mb-6"><button id="loginTab" class="flex-1 pb-3 font-medium border-b-2 text-green-600" style="border-color: #10b981;" onclick="switchAuthTab('login')">Log In</button> <button id="signupTab" class="flex-1 pb-3 font-medium text-gray-500" onclick="switchAuthTab('signup')">Sign Up</button>
      </div><!-- Login Form -->
      <form id="loginForm" class="space-y-4">
       <div><label class="block text-sm font-medium mb-2">Email Address</label> <input type="email" name="email" required class="form-input w-full px-4 py-2 rounded-lg border-2" placeholder="your.email@example.com">
       </div>
       <div><label class="block text-sm font-medium mb-2">Password</label> <input type="password" name="password" required class="form-input w-full px-4 py-2 rounded-lg border-2" placeholder="Enter your password">
       </div>
       <div class="bg-gray-100 p-4 rounded-lg text-center text-sm">
        <p class="font-medium mb-2">Demo Accounts (Click to use):</p><button type="button" onclick="fillDemoAccount('ipmr')" class="hover:underline mr-4" style="color: #10b981;">IPMR Account</button> <button type="button" onclick="fillDemoAccount('chieftain')" class="hover:underline mr-4" style="color: #10b981;">Chieftain Account</button> <button type="button" onclick="fillDemoAccount('admin')" class="hover:underline" style="color: #10b981;">Admin Account</button>
       </div><button type="submit" class="btn w-full py-3 rounded-lg font-medium text-white shadow-md" style="background-color: #10b981;"> Log In </button>
      </form><!-- Signup Form -->
      <form id="signupForm" class="space-y-4 hidden">
       <div><label class="block text-sm font-medium mb-2">Full Name</label> <input type="text" name="fullName" required class="form-input w-full px-4 py-2 rounded-lg border-2" placeholder="Juan Dela Cruz">
       </div>
       <div><label class="block text-sm font-medium mb-2">Email Address</label> <input type="email" name="email" required class="form-input w-full px-4 py-2 rounded-lg border-2" placeholder="your.email@example.com">
       </div>
       <div><label class="block text-sm font-medium mb-2">Password</label> <input type="password" name="password" required class="form-input w-full px-4 py-2 rounded-lg border-2" placeholder="Create a password">
       </div>
       <div><label class="block text-sm font-medium mb-2">Confirm Password</label> <input type="password" name="confirmPassword" required class="form-input w-full px-4 py-2 rounded-lg border-2" placeholder="Confirm your password">
       </div>
       <div><label class="block text-sm font-medium mb-2">User Role</label> <select name="userRole" required class="form-input w-full px-4 py-2 rounded-lg border-2"> <option value="">Select Role</option> <option value="IPMR">IPMR (Indigenous Peoples Mandatory Representative)</option> <option value="Chieftain">Chieftain</option> </select>
       </div>
       <div class="bg-blue-50 p-4 rounded-lg text-sm">
        <p class="text-blue-800">📧 Email confirmation will be required after registration</p>
       </div><button type="submit" class="btn w-full py-3 rounded-lg font-medium text-white shadow-md" style="background-color: #10b981;"> Create Account </button>
      </form>
     </div>
    </div>
   </div><!-- Main Application (Hidden until logged in) -->
   <div id="mainApp" class="flex h-full hidden"><!-- Sidebar -->
    <aside id="sidebar" class="w-64 shadow-lg flex flex-col" style="background-color: #1e40af;">
     <div class="p-6 border-b border-white border-opacity-20">
      <div class="flex items-center mb-3">
       <svg width="40" height="40" viewbox="0 0 120 120" xmlns="http://www.w3.org/2000/svg" class="mr-3"><path d="M60 10 L100 30 L100 70 Q100 90 60 110 Q20 90 20 70 L20 30 Z" fill="#fbbf24" stroke="#f59e0b" stroke-width="2" /> <path d="M40 50 L50 35 L60 50 L70 35 L80 50" fill="none" stroke="#059669" stroke-width="3" stroke-linecap="round" />
       </svg>
       <div>
        <h1 id="sidebarSystemTitle" class="text-lg font-bold text-white">BANTAY LAHI</h1>
        <p class="text-xs text-white text-opacity-80">v1.0</p>
       </div>
      </div>
      <div class="text-sm text-white text-opacity-90">
       <p class="font-medium" id="currentUserName">User Name</p>
       <p class="text-xs opacity-75" id="currentUserRole">Role</p>
      </div>
     </div>
     <nav class="flex-1 p-4 overflow-y-auto" id="navigationMenu"><!-- Navigation will be populated based on user role -->
     </nav>
     <div class="p-4 border-t border-white border-opacity-20"><button onclick="logout()" class="w-full text-left px-4 py-3 rounded-lg text-white hover:bg-white hover:bg-opacity-10"> <span class="text-lg mr-3">🚪</span> Log Out </button>
     </div>
    </aside><!-- Main Content -->
    <main class="flex-1 overflow-auto" style="background-color: #f3f4f6;"><!-- Dashboard View (IPMR) -->
     <div id="dashboardView" class="p-8 hidden">
      <div class="mb-8">
       <h2 class="text-3xl font-bold mb-2">Administrative Dashboard</h2>
       <p class="opacity-75">Welcome to BANTAY LAHI Information System</p>
      </div><!-- Statistics Cards -->
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-8">
       <div class="stat-card bg-white rounded-xl p-6 shadow-md">
        <div class="flex items-center justify-between mb-2"><span class="text-4xl">👥</span> <span class="text-sm font-medium opacity-75">Total</span>
        </div>
        <div class="text-3xl font-bold" id="totalPopulation">
         0
        </div>
        <div class="text-sm opacity-75 mt-1">
         Total Population
        </div>
       </div>
       <div class="stat-card bg-white rounded-xl p-6 shadow-md">
        <div class="flex items-center justify-between mb-2"><span class="text-4xl">🏘️</span> <span class="text-sm font-medium opacity-75">Total</span>
        </div>
        <div class="text-3xl font-bold" id="totalBarangays">
         0
        </div>
        <div class="text-sm opacity-75 mt-1">
         Barangays
        </div>
       </div>
       <div class="stat-card bg-white rounded-xl p-6 shadow-md">
        <div class="flex items-center justify-between mb-2"><span class="text-4xl">🏠</span> <span class="text-sm font-medium opacity-75">Total</span>
        </div>
        <div class="text-3xl font-bold" id="totalHouseholds">
         0
        </div>
        <div class="text-sm opacity-75 mt-1">
         Households
        </div>
       </div>
       <div class="stat-card bg-white rounded-xl p-6 shadow-md">
        <div class="flex items-center justify-between mb-2"><span class="text-4xl">🌍</span> <span class="text-sm font-medium opacity-75">Groups</span>
        </div>
        <div class="text-3xl font-bold" id="totalGroups">
         0
        </div>
        <div class="text-sm opacity-75 mt-1">
         Indigenous Groups
        </div>
       </div>
      </div><!-- Recent Activities -->
      <div class="bg-white rounded-xl shadow-md p-6 mb-8">
       <h3 class="text-xl font-bold mb-4">Recent Activities / Latest Data Entry</h3>
       <div id="recentActivities" class="space-y-3">
        <p class="text-center py-8 opacity-50">No recent activities</p>
       </div>
      </div><!-- Location Map -->
      <div class="bg-white rounded-xl shadow-md p-6">
       <h3 class="text-xl font-bold mb-4">📍 Location Map of Catanauan, Quezon</h3>
       <div class="rounded-lg overflow-hidden" style="height: 500px;"><iframe src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d62345.89876543211!2d122.3167!3d13.5833!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x33a1c8f8f8f8f8f8%3A0x1234567890abcdef!2sCatanauan%2C%20Quezon!5e0!3m2!1sen!2sph!4v1234567890123!5m2!1sen!2sph" width="100%" height="100%" style="border:0;" allowfullscreen loading="lazy" referrerpolicy="no-referrer-when-downgrade"> </iframe>
       </div>
       <p class="text-sm text-gray-600 mt-4">📌 Catanauan is a coastal municipality in Quezon Province, Philippines, home to indigenous communities including Agta and Dumagat peoples.</p>
      </div>
     </div><!-- Barangays View -->
     <div id="barangaysView" class="p-8 hidden">
      <div class="mb-6">
       <h2 class="text-3xl font-bold mb-2">List of Barangays</h2>
       <p class="opacity-75">View members by barangay</p>
      </div>
      <div id="barangaysGrid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-4"><!-- Barangays will be populated here -->
      </div>
     </div><!-- Community Masterlist View -->
     <div id="masterlistView" class="p-8 hidden">
      <div class="flex justify-between items-center mb-6">
       <div>
        <h2 class="text-3xl font-bold mb-2">Community Masterlist</h2>
        <p class="opacity-75">Complete database of community members</p>
       </div><button id="addMemberBtn" onclick="openAddMemberModal()" class="btn px-6 py-3 rounded-lg font-medium text-white shadow-md" style="background-color: #10b981;"> ➕ Add New Member </button>
      </div><!-- Search and Filter -->
      <div class="bg-white rounded-xl shadow-md p-6 mb-6">
       <div class="flex gap-4 items-center"><input type="text" id="searchMembers" placeholder="Search by name..." class="form-input flex-1 px-4 py-2 rounded-lg border-2" oninput="filterMembers()"> <button onclick="toggleFilterPanel()" class="btn px-6 py-2 rounded-lg font-medium text-white shadow-md flex items-center gap-2" style="background-color: #10b981;"> <span class="text-xl">🔍</span> <span>Filters</span> <span id="activeFilterCount" class="hidden px-2 py-1 bg-white text-green-600 rounded-full text-xs font-bold"></span> </button> <button id="clearFiltersBtn" onclick="clearAllFilters()" class="btn px-4 py-2 rounded-lg font-medium border-2 text-red-600 border-red-600 hidden"> Clear All </button>
       </div><!-- Filter Panel (Hidden by default) -->
       <div id="filterPanel" class="hidden mt-4 pt-4 border-t">
        <h4 class="font-bold mb-4 text-lg">📋 Select Filters to Apply</h4>
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4">
         <div><label class="block text-sm font-medium mb-2">Barangay</label> <select id="filterBarangay" class="form-input w-full px-4 py-2 rounded-lg border-2" onchange="filterMembers()"> <option value="">All Barangays</option> </select>
         </div>
         <div><label class="block text-sm font-medium mb-2">Sex</label> <select id="filterSex" class="form-input w-full px-4 py-2 rounded-lg border-2" onchange="filterMembers()"> <option value="">All Genders</option> <option value="Male">Male</option> <option value="Female">Female</option> </select>
         </div>
         <div><label class="block text-sm font-medium mb-2">Civil Status</label> <select id="filterCivilStatus" class="form-input w-full px-4 py-2 rounded-lg border-2" onchange="filterMembers()"> <option value="">All Civil Status</option> <option value="Single">Single</option> <option value="Married">Married</option> <option value="Widowed">Widowed</option> <option value="Separated">Separated</option> <option value="Others">Others</option> </select>
         </div>
         <div><label class="block text-sm font-medium mb-2">Indigenous Group</label> <select id="filterGroup" class="form-input w-full px-4 py-2 rounded-lg border-2" onchange="filterMembers()"> <option value="">All Indigenous Groups</option> </select>
         </div>
         <div><label class="block text-sm font-medium mb-2">Age Range</label> <select id="filterAge" class="form-input w-full px-4 py-2 rounded-lg border-2" onchange="filterMembers()"> <option value="">All Ages</option> <option value="0-17">0-17 (Minor)</option> <option value="18-35">18-35 (Young Adult)</option> <option value="36-59">36-59 (Adult)</option> <option value="60+">60+ (Senior)</option> </select>
         </div>
         <div><label class="block text-sm font-medium mb-2">Education Level</label> <select id="filterEducation" class="form-input w-full px-4 py-2 rounded-lg border-2" onchange="filterMembers()"> <option value="">All Education Levels</option> <option value="No Formal Education">No Formal Education</option> <option value="Elementary">Elementary</option> <option value="High School">High School</option> <option value="College Level">College Level</option> <option value="College Graduate">College Graduate</option> <option value="Vocational/Technical">Vocational/Technical</option> <option value="Postgraduate">Postgraduate</option> </select>
         </div>
         <div><label class="block text-sm font-medium mb-2">Household Relation</label> <select id="filterRelation" class="form-input w-full px-4 py-2 rounded-lg border-2" onchange="filterMembers()"> <option value="">All Relations</option> <option value="Head">Head</option> <option value="Spouse">Spouse</option> <option value="Child">Child</option> <option value="Parent">Parent</option> <option value="Sibling">Sibling</option> <option value="Grandchild">Grandchild</option> <option value="Other Relative">Other Relative</option> </select>
         </div>
         <div><label class="block text-sm font-medium mb-2">Religion</label> <select id="filterReligion" class="form-input w-full px-4 py-2 rounded-lg border-2" onchange="filterMembers()"> <option value="">All Religions</option> </select>
         </div>
        </div>
       </div>
      </div><!-- Members Table -->
      <div class="bg-white rounded-xl shadow-md overflow-hidden">
       <div class="overflow-x-auto">
        <table class="w-full">
         <thead class="bg-gray-50">
          <tr class="border-b-2">
           <th class="px-4 py-3 text-left font-semibold text-sm">Photo</th>
           <th class="px-4 py-3 text-left font-semibold text-sm">Full Name</th>
           <th class="px-4 py-3 text-left font-semibold text-sm">Age</th>
           <th class="px-4 py-3 text-left font-semibold text-sm">Sex</th>
           <th class="px-4 py-3 text-left font-semibold text-sm">Civil Status</th>
           <th class="px-4 py-3 text-left font-semibold text-sm">Address</th>
           <th class="px-4 py-3 text-left font-semibold text-sm">Barangay</th>
           <th class="px-4 py-3 text-left font-semibold text-sm">Contact</th>
           <th class="px-4 py-3 text-left font-semibold text-sm">Education</th>
           <th class="px-4 py-3 text-left font-semibold text-sm">Occupation</th>
           <th class="px-4 py-3 text-left font-semibold text-sm">Indigenous Group</th>
           <th class="px-4 py-3 text-left font-semibold text-sm">Bloodline %</th>
           <th class="px-4 py-3 text-left font-semibold text-sm">Actions</th>
          </tr>
         </thead>
         <tbody id="membersTableBody">
          <tr>
           <td colspan="13" class="px-6 py-8 text-center opacity-50">No members registered yet</td>
          </tr>
         </tbody>
        </table>
       </div>
      </div>
     </div><!-- Household Tracking View -->
     <div id="householdView" class="p-8 hidden">
      <div class="mb-6">
       <h2 class="text-3xl font-bold mb-2">Household and Lineage Tracking</h2>
       <p class="opacity-75">View family trees and household relationships</p>
      </div>
      <div id="householdsContainer" class="space-y-6">
       <div class="bg-white rounded-xl shadow-md p-6 text-center opacity-50">
        <p class="py-8">No households registered yet</p>
       </div>
      </div>
     </div><!-- Tribe Distribution View -->
     <div id="tribeView" class="p-8 hidden">
      <div class="mb-6">
       <h2 class="text-3xl font-bold mb-2">Tribe Distribution</h2>
       <p class="opacity-75">Bloodline percentage analysis of indigenous groups</p>
      </div>
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
       <div class="bg-white rounded-xl shadow-md p-6">
        <h3 class="text-xl font-bold mb-4">Indigenous Group Distribution</h3>
        <div id="tribeChart" class="space-y-4">
         <p class="text-center py-8 opacity-50">No tribe data available</p>
        </div>
       </div>
       <div class="bg-white rounded-xl shadow-md p-6">
        <h3 class="text-xl font-bold mb-4">Bloodline Percentages</h3>
        <div id="bloodlineChart" class="space-y-4">
         <p class="text-center py-8 opacity-50">No bloodline data available</p>
        </div>
       </div>
      </div>
     </div><!-- Admin View (Main Administrator) -->
     <div id="adminView" class="p-8 hidden">
      <div class="mb-6">
       <h2 class="text-3xl font-bold mb-2">Administrator Dashboard</h2>
       <p class="opacity-75">System overview and user management</p>
      </div>
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-6 mb-6">
       <div class="bg-white rounded-xl shadow-md p-6">
        <h3 class="text-xl font-bold mb-4">System Statistics</h3>
        <div class="space-y-3">
         <div class="flex justify-between items-center p-3 bg-gray-50 rounded"><span class="font-medium">Total Users</span> <span class="text-2xl font-bold" id="adminTotalUsers">3</span>
         </div>
         <div class="flex justify-between items-center p-3 bg-gray-50 rounded"><span class="font-medium">Total Members</span> <span class="text-2xl font-bold" id="adminTotalMembers">0</span>
         </div>
         <div class="flex justify-between items-center p-3 bg-gray-50 rounded"><span class="font-medium">Database Size</span> <span class="text-2xl font-bold" id="adminDbSize">0 KB</span>
         </div>
        </div>
       </div>
       <div class="bg-white rounded-xl shadow-md p-6">
        <h3 class="text-xl font-bold mb-4">User Accounts</h3>
        <div class="space-y-2">
         <div class="flex items-center justify-between p-3 border rounded">
          <div>
           <p class="font-medium">IPMR Account</p>
           <p class="text-sm opacity-75">ipmr@bantaylahi.com</p>
          </div><span class="px-3 py-1 bg-blue-100 text-blue-800 rounded-full text-sm">Active</span>
         </div>
         <div class="flex items-center justify-between p-3 border rounded">
          <div>
           <p class="font-medium">Chieftain Account</p>
           <p class="text-sm opacity-75">chieftain@bantaylahi.com</p>
          </div><span class="px-3 py-1 bg-blue-100 text-blue-800 rounded-full text-sm">Active</span>
         </div>
         <div class="flex items-center justify-between p-3 border rounded">
          <div>
           <p class="font-medium">Admin Account</p>
           <p class="text-sm opacity-75">admin@bantaylahi.com</p>
          </div><span class="px-3 py-1 bg-blue-100 text-blue-800 rounded-full text-sm">Active</span>
         </div>
        </div>
       </div>
      </div>
      <div class="bg-white rounded-xl shadow-md p-6">
       <h3 class="text-xl font-bold mb-4">Login History</h3>
       <div class="overflow-x-auto">
        <table class="w-full">
         <thead class="bg-gray-50">
          <tr class="border-b">
           <th class="px-4 py-3 text-left font-semibold">User</th>
           <th class="px-4 py-3 text-left font-semibold">Role</th>
           <th class="px-4 py-3 text-left font-semibold">Login Time</th>
           <th class="px-4 py-3 text-left font-semibold">Status</th>
          </tr>
         </thead>
         <tbody id="loginHistoryBody">
          <tr>
           <td colspan="4" class="px-4 py-8 text-center opacity-50">No login history available</td>
          </tr>
         </tbody>
        </table>
       </div>
      </div>
     </div>
    </main>
   </div>
  </div><!-- Add Member Modal -->
  <div id="addMemberModal" class="fixed inset-0 modal-backdrop hidden items-center justify-center p-4" style="z-index: 1000;">
   <div class="modal-content bg-white rounded-xl shadow-2xl max-w-5xl w-full max-h-[90%] overflow-y-auto">
    <div class="p-6 border-b text-white rounded-t-xl" style="background-color: #10b981;">
     <h3 class="text-2xl font-bold">Add New Community Member</h3>
    </div>
    <form id="addMemberForm" class="p-6"><!-- Photo Section -->
     <div class="mb-6 pb-6 border-b">
      <h4 class="font-bold text-lg mb-4">📸 Member Photo</h4>
      <div class="flex flex-col items-center gap-4">
       <div id="photoPreviewContainer" class="hidden"><img id="photoPreview" class="photo-preview border-2 border-gray-300" alt="Member photo">
       </div>
       <div class="flex gap-2"><button type="button" onclick="startCamera()" class="btn px-4 py-2 rounded-lg font-medium text-white" style="background-color: #10b981;"> 📷 Take Photo with Camera </button> <button type="button" id="clearPhotoBtn" onclick="clearPhoto()" class="btn px-4 py-2 rounded-lg font-medium border-2 text-red-600 border-red-600 hidden"> ✕ Clear Photo </button>
       </div>
       <p class="text-sm text-gray-600 mt-2">ℹ️ <strong>Camera Access:</strong> Your browser will ask for camera permission. Click "Allow" to take photos.</p>
      </div>
     </div>
     <div class="grid grid-cols-1 md:grid-cols-2 gap-6"><!-- Personal Information -->
      <div class="md:col-span-2">
       <h4 class="font-bold text-lg mb-4 text-blue-600">Personal Information</h4>
      </div>
      <div><label class="block text-sm font-medium mb-2">Last Name *</label> <input type="text" name="lastName" required class="form-input w-full px-4 py-2 rounded-lg border-2">
      </div>
      <div><label class="block text-sm font-medium mb-2">First Name *</label> <input type="text" name="firstName" required class="form-input w-full px-4 py-2 rounded-lg border-2">
      </div>
      <div><label class="block text-sm font-medium mb-2">Middle Name</label> <input type="text" name="middleName" class="form-input w-full px-4 py-2 rounded-lg border-2">
      </div>
      <div><label class="block text-sm font-medium mb-2">Date of Birth *</label> <input type="date" name="dateOfBirth" required class="form-input w-full px-4 py-2 rounded-lg border-2" onchange="calculateAge()">
      </div>
      <div><label class="block text-sm font-medium mb-2">Age *</label> <input type="number" name="age" id="ageInput" required readonly class="form-input w-full px-4 py-2 rounded-lg border-2 bg-gray-50">
      </div>
      <div><label class="block text-sm font-medium mb-2">Sex *</label> <select name="sex" required class="form-input w-full px-4 py-2 rounded-lg border-2"> <option value="">Select Sex</option> <option value="Male">Male</option> <option value="Female">Female</option> </select>
      </div>
      <div><label class="block text-sm font-medium mb-2">Civil Status *</label> <select name="civilStatus" required class="form-input w-full px-4 py-2 rounded-lg border-2"> <option value="">Select Status</option> <option value="Single">Single</option> <option value="Married">Married</option> <option value="Widowed">Widowed</option> <option value="Separated">Separated</option> <option value="Others">Others</option> </select>
      </div>
      <div><label class="block text-sm font-medium mb-2">Nationality *</label> <input type="text" name="nationality" required class="form-input w-full px-4 py-2 rounded-lg border-2" value="Filipino">
      </div>
      <div><label class="block text-sm font-medium mb-2">Religion</label> <input type="text" name="religion" class="form-input w-full px-4 py-2 rounded-lg border-2">
      </div><!-- Address Information -->
      <div class="md:col-span-2 mt-4">
       <h4 class="font-bold text-lg mb-4 text-blue-600">Address and Contact Information</h4>
      </div>
      <div class="md:col-span-2"><label class="block text-sm font-medium mb-2">Complete Address *</label> <input type="text" name="completeAddress" required class="form-input w-full px-4 py-2 rounded-lg border-2">
      </div>
      <div><label class="block text-sm font-medium mb-2">Barangay *</label> <select name="barangay" required class="form-input w-full px-4 py-2 rounded-lg border-2"> <option value="">Select Barangay</option> <option value="Anusan">Anusan</option> <option value="Barangay 1">Barangay 1</option> <option value="Barangay 2">Barangay 2</option> <option value="Barangay 3">Barangay 3</option> <option value="Barangay 4">Barangay 4</option> <option value="Barangay 5">Barangay 5</option> <option value="Barangay 6">Barangay 6</option> <option value="Barangay 7">Barangay 7</option> <option value="Barangay 8">Barangay 8</option> <option value="Barangay 9">Barangay 9</option> <option value="Barangay 10">Barangay 10</option> <option value="Bolo">Bolo</option> <option value="Bulagsong">Bulagsong</option> <option value="Camandiison">Camandiison</option> <option value="Canculajao">Canculajao</option> <option value="Catumbo">Catumbo</option> <option value="Cawayanin Ibaba">Cawayanin Ibaba</option> <option value="Cawayanin Ilaya">Cawayanin Ilaya</option> <option value="Cutcutan">Cutcutan</option> <option value="Dahican">Dahican</option> <option value="Doongan Ibaba">Doongan Ibaba</option> <option value="Doongan Ilaya">Doongan Ilaya</option> <option value="Macpac">Macpac</option> <option value="Madulao">Madulao</option> <option value="Matandang Sabang Kanluran">Matandang Sabang Kanluran</option> <option value="Matandang Sabang Silangan">Matandang Sabang Silangan</option> <option value="Milagros">Milagros</option> <option value="Navitas">Navitas</option> <option value="Pacabit">Pacabit</option> <option value="San Antonio Magkupa">San Antonio Magkupa</option> <option value="San Antonio Pala">San Antonio Pala</option> <option value="San Isidro">San Isidro</option> <option value="San Jose Anyao">San Jose Anyao</option> <option value="San Pablo">San Pablo</option> <option value="San Roque">San Roque</option> <option value="San Vicente Kanluran">San Vicente Kanluran</option> <option value="San Vicente Silangan">San Vicente Silangan</option> <option value="Santa Maria">Santa Maria</option> <option value="Tagabas Ibaba">Tagabas Ibaba</option> <option value="Tagabas Ilaya">Tagabas Ilaya</option> <option value="Tagbacan Ibaba">Tagbacan Ibaba</option> <option value="Tagbacan Ilaya">Tagbacan Ilaya</option> <option value="Tagbacan Silangan">Tagbacan Silangan</option> <option value="Tuhian">Tuhian</option> </select>
      </div>
      <div><label class="block text-sm font-medium mb-2">Municipality/City *</label> <input type="text" name="municipality" required class="form-input w-full px-4 py-2 rounded-lg border-2" value="Catanauan">
      </div>
      <div><label class="block text-sm font-medium mb-2">Province *</label> <input type="text" name="province" required class="form-input w-full px-4 py-2 rounded-lg border-2" value="Quezon">
      </div>
      <div><label class="block text-sm font-medium mb-2">ZIP Code *</label> <input type="text" name="zipCode" required class="form-input w-full px-4 py-2 rounded-lg border-2" value="4311">
      </div>
      <div><label class="block text-sm font-medium mb-2">Contact Number</label> <input type="tel" name="contactNumber" class="form-input w-full px-4 py-2 rounded-lg border-2" placeholder="+63">
      </div>
      <div><label class="block text-sm font-medium mb-2">Email Address</label> <input type="email" name="email" class="form-input w-full px-4 py-2 rounded-lg border-2">
      </div><!-- Education -->
      <div class="md:col-span-2 mt-4">
       <h4 class="font-bold text-lg mb-4 text-blue-600">Education and Occupation</h4>
      </div>
      <div><label class="block text-sm font-medium mb-2">Highest Educational Attainment</label> <select name="educationLevel" class="form-input w-full px-4 py-2 rounded-lg border-2"> <option value="">Select Education Level</option> <option value="No Formal Education">No Formal Education</option> <option value="Elementary">Elementary</option> <option value="High School">High School</option> <option value="College Level">College Level</option> <option value="College Graduate">College Graduate</option> <option value="Vocational/Technical">Vocational/Technical</option> <option value="Postgraduate">Postgraduate</option> </select>
      </div>
      <div><label class="block text-sm font-medium mb-2">Occupation</label> <input type="text" name="occupation" class="form-input w-full px-4 py-2 rounded-lg border-2" placeholder="If student, specify school">
      </div><!-- Household Information -->
      <div class="md:col-span-2 mt-4">
       <h4 class="font-bold text-lg mb-4 text-blue-600">Household Information</h4>
      </div>
      <div><label class="block text-sm font-medium mb-2">Household ID</label> <input type="text" name="householdId" class="form-input w-full px-4 py-2 rounded-lg border-2" placeholder="e.g., HH-001">
      </div>
      <div><label class="block text-sm font-medium mb-2">Relation to Household Head</label> <select name="relationToHead" class="form-input w-full px-4 py-2 rounded-lg border-2"> <option value="">Select Relation</option> <option value="Head">Head</option> <option value="Spouse">Spouse</option> <option value="Child">Child</option> <option value="Parent">Parent</option> <option value="Sibling">Sibling</option> <option value="Grandchild">Grandchild</option> <option value="Other Relative">Other Relative</option> </select>
      </div><!-- Cultural Information -->
      <div class="md:col-span-2 mt-4">
       <h4 class="font-bold text-lg mb-4 text-blue-600">Cultural Information &amp; Bloodline Calculator</h4>
      </div>
      <div class="md:col-span-2 bg-blue-50 p-4 rounded-lg mb-4">
       <h5 class="font-bold mb-3">👨‍👩‍👧 Parent's Indigenous Groups (for Bloodline Calculation)</h5>
       <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
        <div><label class="block text-sm font-medium mb-2">Mother's Indigenous Group</label> <select name="motherGroup" id="motherGroup" class="form-input w-full px-4 py-2 rounded-lg border-2" onchange="calculateBloodline()"> <option value="">Select Mother's Group</option> <option value="Aeta">Aeta</option> <option value="Agta">Agta</option> <option value="Ayta">Ayta</option> <option value="Agta (Cagayan Valley)">Agta (Cagayan Valley)</option> <option value="Dumagat">Dumagat</option> <option value="Atta">Atta</option> <option value="Isneg">Isneg</option> <option value="Ibanag">Ibanag</option> <option value="Itawes">Itawes</option> <option value="Isinay">Isinay</option> <option value="Ilongot (Bugkalot)">Ilongot (Bugkalot)</option> <option value="Remontado">Remontado</option> <option value="Iraya">Iraya</option> <option value="Alangan">Alangan</option> <option value="Tadyawan">Tadyawan</option> <option value="Tau-buid">Tau-buid</option> <option value="Buhid">Buhid</option> <option value="Hanunuo">Hanunuo</option> <option value="Bangon">Bangon</option> <option value="Ratagnon">Ratagnon</option> <option value="Bontok">Bontok</option> <option value="Ibaloy">Ibaloy</option> <option value="Ifugao">Ifugao</option> <option value="Kalinga">Kalinga</option> <option value="Kankanaey">Kankanaey</option> <option value="Tingguian (Itneg)">Tingguian (Itneg)</option> <option value="Ikalahan (Kalanguya)">Ikalahan (Kalanguya)</option> <option value="Ati">Ati</option> <option value="Bukidnon">Bukidnon</option> <option value="Magahat">Magahat</option> <option value="Ata">Ata</option> <option value="Bagobo">Bagobo</option> <option value="Banwaon">Banwaon</option> <option value="B'laan">B'laan</option> <option value="Dibabawon">Dibabawon</option> <option value="Higaonon">Higaonon</option> <option value="Manobo">Manobo</option> <option value="Mamanwa">Mamanwa</option> <option value="Mandaya">Mandaya</option> <option value="Mansaka">Mansaka</option> <option value="Subanen">Subanen</option> <option value="Tagakaulo">Tagakaulo</option> <option value="Talaandig">Talaandig</option> <option value="Teduray">Teduray</option> <option value="Ubo / Obu-Manuvu">Ubo / Obu-Manuvu</option> <option value="Badjao">Badjao</option> <option value="Maranao">Maranao</option> <option value="Maguindanaon">Maguindanaon</option> <option value="Tausug">Tausug</option> <option value="Sama">Sama</option> <option value="Yakan">Yakan</option> </select>
        </div>
        <div><label class="block text-sm font-medium mb-2">Father's Indigenous Group</label> <select name="fatherGroup" id="fatherGroup" class="form-input w-full px-4 py-2 rounded-lg border-2" onchange="calculateBloodline()"> <option value="">Select Father's Group</option> <option value="Aeta">Aeta</option> <option value="Agta">Agta</option> <option value="Ayta">Ayta</option> <option value="Agta (Cagayan Valley)">Agta (Cagayan Valley)</option> <option value="Dumagat">Dumagat</option> <option value="Atta">Atta</option> <option value="Isneg">Isneg</option> <option value="Ibanag">Ibanag</option> <option value="Itawes">Itawes</option> <option value="Isinay">Isinay</option> <option value="Ilongot (Bugkalot)">Ilongot (Bugkalot)</option> <option value="Remontado">Remontado</option> <option value="Iraya">Iraya</option> <option value="Alangan">Alangan</option> <option value="Tadyawan">Tadyawan</option> <option value="Tau-buid">Tau-buid</option> <option value="Buhid">Buhid</option> <option value="Hanunuo">Hanunuo</option> <option value="Bangon">Bangon</option> <option value="Ratagnon">Ratagnon</option> <option value="Bontok">Bontok</option> <option value="Ibaloy">Ibaloy</option> <option value="Ifugao">Ifugao</option> <option value="Kalinga">Kalinga</option> <option value="Kankanaey">Kankanaey</option> <option value="Tingguian (Itneg)">Tingguian (Itneg)</option> <option value="Ikalahan (Kalanguya)">Ikalahan (Kalanguya)</option> <option value="Ati">Ati</option> <option value="Bukidnon">Bukidnon</option> <option value="Magahat">Magahat</option> <option value="Ata">Ata</option> <option value="Bagobo">Bagobo</option> <option value="Banwaon">Banwaon</option> <option value="B'laan">B'laan</option> <option value="Dibabawon">Dibabawon</option> <option value="Higaonon">Higaonon</option> <option value="Manobo">Manobo</option> <option value="Mamanwa">Mamanwa</option> <option value="Mandaya">Mandaya</option> <option value="Mansaka">Mansaka</option> <option value="Subanen">Subanen</option> <option value="Tagakaulo">Tagakaulo</option> <option value="Talaandig">Talaandig</option> <option value="Teduray">Teduray</option> <option value="Ubo / Obu-Manuvu">Ubo / Obu-Manuvu</option> <option value="Badjao">Badjao</option> <option value="Maranao">Maranao</option> <option value="Maguindanaon">Maguindanaon</option> <option value="Tausug">Tausug</option> <option value="Sama">Sama</option> <option value="Yakan">Yakan</option> </select>
        </div>
       </div>
       <div class="mt-3 p-3 bg-white rounded border-2 border-blue-300">
        <p class="text-sm font-medium mb-1">📊 Calculated Bloodline:</p>
        <p id="calculatedBloodline" class="text-lg font-bold text-blue-600">Enter parent's groups to calculate</p>
       </div>
      </div>
      <div><label class="block text-sm font-medium mb-2">Member's Primary Indigenous Group *</label> <select name="indigenousGroup" id="indigenousGroup" required class="form-input w-full px-4 py-2 rounded-lg border-2"> <option value="">Select Indigenous Group</option> <option value="Aeta">Aeta</option> <option value="Agta">Agta</option> <option value="Ayta">Ayta</option> <option value="Agta (Cagayan Valley)">Agta (Cagayan Valley)</option> <option value="Dumagat">Dumagat</option> <option value="Atta">Atta</option> <option value="Isneg">Isneg</option> <option value="Ibanag">Ibanag</option> <option value="Itawes">Itawes</option> <option value="Isinay">Isinay</option> <option value="Ilongot (Bugkalot)">Ilongot (Bugkalot)</option> <option value="Remontado">Remontado</option> <option value="Iraya">Iraya</option> <option value="Alangan">Alangan</option> <option value="Tadyawan">Tadyawan</option> <option value="Tau-buid">Tau-buid</option> <option value="Buhid">Buhid</option> <option value="Hanunuo">Hanunuo</option> <option value="Bangon">Bangon</option> <option value="Ratagnon">Ratagnon</option> <option value="Bontok">Bontok</option> <option value="Ibaloy">Ibaloy</option> <option value="Ifugao">Ifugao</option> <option value="Kalinga">Kalinga</option> <option value="Kankanaey">Kankanaey</option> <option value="Tingguian (Itneg)">Tingguian (Itneg)</option> <option value="Ikalahan (Kalanguya)">Ikalahan (Kalanguya)</option> <option value="Ati">Ati</option> <option value="Bukidnon">Bukidnon</option> <option value="Magahat">Magahat</option> <option value="Ata">Ata</option> <option value="Bagobo">Bagobo</option> <option value="Banwaon">Banwaon</option> <option value="B'laan">B'laan</option> <option value="Dibabawon">Dibabawon</option> <option value="Higaonon">Higaonon</option> <option value="Manobo">Manobo</option> <option value="Mamanwa">Mamanwa</option> <option value="Mandaya">Mandaya</option> <option value="Mansaka">Mansaka</option> <option value="Subanen">Subanen</option> <option value="Tagakaulo">Tagakaulo</option> <option value="Talaandig">Talaandig</option> <option value="Teduray">Teduray</option> <option value="Ubo / Obu-Manuvu">Ubo / Obu-Manuvu</option> <option value="Badjao">Badjao</option> <option value="Maranao">Maranao</option> <option value="Maguindanaon">Maguindanaon</option> <option value="Tausug">Tausug</option> <option value="Sama">Sama</option> <option value="Yakan">Yakan</option> </select>
      </div>
      <div><label class="block text-sm font-medium mb-2">Bloodline Percentage (Auto-calculated)</label> <input type="text" name="bloodlinePercentage" id="bloodlinePercentage" readonly class="form-input w-full px-4 py-2 rounded-lg border-2 bg-gray-50" placeholder="Will be calculated from parents">
      </div>
      <div class="md:col-span-2"><label class="block text-sm font-medium mb-2">Languages Spoken</label> <input type="text" name="languages" class="form-input w-full px-4 py-2 rounded-lg border-2" placeholder="e.g., Tagalog, English, Agta">
      </div>
     </div>
     <div class="flex justify-end gap-4 mt-6 pt-6 border-t"><button type="button" onclick="closeAddMemberModal()" class="btn px-6 py-2 rounded-lg font-medium border-2"> Cancel </button> <button type="submit" id="submitMemberBtn" class="btn px-6 py-2 rounded-lg font-medium text-white shadow-md" style="background-color: #10b981;"> Add Member </button>
     </div>
    </form>
   </div>
  </div><!-- Camera Modal -->
  <div id="cameraModal" class="fixed inset-0 modal-backdrop hidden items-center justify-center p-4" style="z-index: 1001;">
   <div class="modal-content bg-white rounded-xl shadow-2xl max-w-2xl w-full p-6">
    <h3 class="text-2xl font-bold mb-4">Take Photo</h3>
    <div class="camera-container mb-4">
     <video id="cameraVideo" autoplay playsinline></video>
     <canvas id="cameraCanvas" class="hidden"></canvas>
    </div>
    <div class="flex justify-end gap-4"><button type="button" onclick="stopCamera()" class="btn px-6 py-2 rounded-lg font-medium border-2"> Cancel </button> <button type="button" onclick="capturePhoto()" class="btn px-6 py-2 rounded-lg font-medium text-white shadow-md" style="background-color: #10b981;"> 📷 Capture </button>
    </div>
   </div>
  </div><!-- View Member Modal -->
  <div id="viewMemberModal" class="fixed inset-0 modal-backdrop hidden items-center justify-center p-4" style="z-index: 1000;">
   <div class="modal-content bg-white rounded-xl shadow-2xl max-w-4xl w-full max-h-[90%] overflow-y-auto">
    <div class="p-6 border-b text-white" style="background-color: #10b981;">
     <h3 class="text-2xl font-bold">Member Details</h3>
    </div>
    <div id="memberDetailsContent" class="p-6"><!-- Content will be populated dynamically -->
    </div>
    <div class="flex justify-end gap-4 p-6 border-t"><button type="button" onclick="closeViewMemberModal()" class="btn px-6 py-2 rounded-lg font-medium border-2"> Close </button> <button type="button" id="editMemberBtn" class="btn px-6 py-2 rounded-lg font-medium text-white shadow-md hidden" style="background-color: #10b981;"> Edit Member </button> <button type="button" id="deleteMemberBtn" class="btn px-6 py-2 rounded-lg font-medium text-white shadow-md hidden" style="background-color: #ef4444;"> Delete Member </button>
    </div>
   </div>
  </div>
  <script>
    // Configuration
    const defaultConfig = {
      background_color: '#059669',
      surface_color: '#ffffff',
      text_color: '#1f2937',
      primary_action_color: '#10b981',
      secondary_action_color: '#6b7280',
      system_title: 'BANTAY LAHI',
      system_subtitle: 'Indigenous Community Information System',
      location_label: 'Catanauan, Quezon',
      font_family: 'Inter',
      font_size: 16
    };

    // State
    let allMembers = [];
    let currentUser = null;
    let currentView = '';
    let selectedMember = null;
    let cameraStream = null;
    let capturedPhotoData = null;

    const BARANGAYS = [
      'Anusan', 'Barangay 1', 'Barangay 2', 'Barangay 3', 'Barangay 4', 'Barangay 5',
      'Barangay 6', 'Barangay 7', 'Barangay 8', 'Barangay 9', 'Barangay 10',
      'Bolo', 'Bulagsong', 'Camandiison', 'Canculajao', 'Catumbo',
      'Cawayanin Ibaba', 'Cawayanin Ilaya', 'Cutcutan', 'Dahican',
      'Doongan Ibaba', 'Doongan Ilaya', 'Macpac', 'Madulao',
      'Matandang Sabang Kanluran', 'Matandang Sabang Silangan',
      'Milagros', 'Navitas', 'Pacabit', 'San Antonio Magkupa',
      'San Antonio Pala', 'San Isidro', 'San Jose Anyao', 'San Pablo',
      'San Roque', 'San Vicente Kanluran', 'San Vicente Silangan',
      'Santa Maria', 'Tagabas Ibaba', 'Tagabas Ilaya', 'Tagbacan Ibaba',
      'Tagbacan Ilaya', 'Tagbacan Silangan', 'Tuhian'
    ];

    // Demo accounts
    const DEMO_ACCOUNTS = {
      ipmr: { email: 'ipmr@bantaylahi.com', password: 'ipmr123', name: 'IPMR Officer', role: 'IPMR' },
      chieftain: { email: 'chieftain@bantaylahi.com', password: 'chief123', name: 'Tribal Chieftain', role: 'Chieftain' },
      admin: { email: 'admin@bantaylahi.com', password: 'admin123', name: 'System Administrator', role: 'Admin' }
    };

    // Data Handler
    const dataHandler = {
      onDataChanged(data) {
        allMembers = data.filter(item => item.type === 'member');
        updateAllViews();
      }
    };

    // Initialize SDKs
    async function initializeApp() {
      const dataResult = await window.dataSdk.init(dataHandler);
      if (!dataResult.isOk) {
        showToast('Failed to initialize data system', 'error');
        return;
      }

      if (window.elementSdk) {
        window.elementSdk.init({
          defaultConfig,
          onConfigChange: async (config) => {
            const customFont = config.font_family || defaultConfig.font_family;
            const baseFontStack = '-apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif';
            const baseSize = config.font_size || defaultConfig.font_size;

            document.body.style.fontFamily = `${customFont}, ${baseFontStack}`;
            document.body.style.fontSize = `${baseSize}px`;

            const sidebar = document.getElementById('sidebar');
            if (sidebar) {
              sidebar.style.backgroundColor = config.background_color || defaultConfig.background_color;
            }

            document.getElementById('loginSystemTitle').textContent = config.system_title || defaultConfig.system_title;
            document.getElementById('loginSystemSubtitle').textContent = config.system_subtitle || defaultConfig.system_subtitle;
            document.getElementById('loginLocationLabel').textContent = config.location_label || defaultConfig.location_label;
            document.getElementById('sidebarSystemTitle').textContent = config.system_title || defaultConfig.system_title;

            const headings = document.querySelectorAll('h1, h2, h3, h4');
            headings.forEach(h => {
              h.style.fontFamily = `${customFont}, ${baseFontStack}`;
              if (h.tagName === 'H1') h.style.fontSize = `${baseSize * 2}px`;
              if (h.tagName === 'H2') h.style.fontSize = `${baseSize * 1.875}px`;
              if (h.tagName === 'H3') h.style.fontSize = `${baseSize * 1.25}px`;
              if (h.tagName === 'H4') h.style.fontSize = `${baseSize * 1.125}px`;
            });
          },
          mapToCapabilities: (config) => ({
            recolorables: [
              {
                get: () => config.background_color || defaultConfig.background_color,
                set: (value) => {
                  if (window.elementSdk) {
                    window.elementSdk.config.background_color = value;
                    window.elementSdk.setConfig({ background_color: value });
                  }
                }
              },
              {
                get: () => config.surface_color || defaultConfig.surface_color,
                set: (value) => {
                  if (window.elementSdk) {
                    window.elementSdk.config.surface_color = value;
                    window.elementSdk.setConfig({ surface_color: value });
                  }
                }
              },
              {
                get: () => config.text_color || defaultConfig.text_color,
                set: (value) => {
                  if (window.elementSdk) {
                    window.elementSdk.config.text_color = value;
                    window.elementSdk.setConfig({ text_color: value });
                  }
                }
              },
              {
                get: () => config.primary_action_color || defaultConfig.primary_action_color,
                set: (value) => {
                  if (window.elementSdk) {
                    window.elementSdk.config.primary_action_color = value;
                    window.elementSdk.setConfig({ primary_action_color: value });
                  }
                }
              },
              {
                get: () => config.secondary_action_color || defaultConfig.secondary_action_color,
                set: (value) => {
                  if (window.elementSdk) {
                    window.elementSdk.config.secondary_action_color = value;
                    window.elementSdk.setConfig({ secondary_action_color: value });
                  }
                }
              }
            ],
            borderables: [],
            fontEditable: {
              get: () => config.font_family || defaultConfig.font_family,
              set: (value) => {
                if (window.elementSdk) {
                  window.elementSdk.config.font_family = value;
                  window.elementSdk.setConfig({ font_family: value });
                }
              }
            },
            fontSizeable: {
              get: () => config.font_size || defaultConfig.font_size,
              set: (value) => {
                if (window.elementSdk) {
                  window.elementSdk.config.font_size = value;
                  window.elementSdk.setConfig({ font_size: value });
                }
              }
            }
          }),
          mapToEditPanelValues: (config) => new Map([
            ['system_title', config.system_title || defaultConfig.system_title],
            ['system_subtitle', config.system_subtitle || defaultConfig.system_subtitle],
            ['location_label', config.location_label || defaultConfig.location_label]
          ])
        });
      }
    }

    // Authentication Functions
    function switchAuthTab(tab) {
      const loginTab = document.getElementById('loginTab');
      const signupTab = document.getElementById('signupTab');
      const loginForm = document.getElementById('loginForm');
      const signupForm = document.getElementById('signupForm');

      if (tab === 'login') {
        loginTab.classList.add('text-green-600');
        loginTab.classList.remove('text-gray-500');
        loginTab.style.borderColor = '#10b981';
        signupTab.classList.remove('text-green-600');
        signupTab.classList.add('text-gray-500');
        signupTab.style.borderColor = 'transparent';
        loginForm.classList.remove('hidden');
        signupForm.classList.add('hidden');
      } else {
        signupTab.classList.add('text-green-600');
        signupTab.classList.remove('text-gray-500');
        signupTab.style.borderColor = '#10b981';
        loginTab.classList.remove('text-green-600');
        loginTab.classList.add('text-gray-500');
        loginTab.style.borderColor = 'transparent';
        signupForm.classList.remove('hidden');
        loginForm.classList.add('hidden');
      }
    }

    function fillDemoAccount(accountType) {
      const account = DEMO_ACCOUNTS[accountType];
      const form = document.getElementById('loginForm');
      form.email.value = account.email;
      form.password.value = account.password;
    }

    document.getElementById('loginForm').addEventListener('submit', (e) => {
      e.preventDefault();
      const formData = new FormData(e.target);
      const email = formData.get('email');
      const password = formData.get('password');

      // Check demo accounts
      const account = Object.values(DEMO_ACCOUNTS).find(acc => acc.email === email && acc.password === password);
      
      if (account) {
        currentUser = account;
        document.getElementById('currentUserName').textContent = account.name;
        document.getElementById('currentUserRole').textContent = account.role;
        
        document.getElementById('loginScreen').classList.add('hidden');
        document.getElementById('mainApp').classList.remove('hidden');
        
        setupNavigation(account.role);
        showToast(`Welcome, ${account.name}!`, 'success');
      } else {
        showToast('Invalid email or password', 'error');
      }
    });

    document.getElementById('signupForm').addEventListener('submit', (e) => {
      e.preventDefault();
      const formData = new FormData(e.target);
      const password = formData.get('password');
      const confirmPassword = formData.get('confirmPassword');

      if (password !== confirmPassword) {
        showToast('Passwords do not match', 'error');
        return;
      }

      showToast('Account created! Please check your email for confirmation.', 'success');
      setTimeout(() => {
        switchAuthTab('login');
        e.target.reset();
      }, 2000);
    });

    function setupNavigation(role) {
      const nav = document.getElementById('navigationMenu');
      
      if (role === 'IPMR') {
        nav.innerHTML = `
          <button class="nav-item active w-full text-left px-4 py-3 rounded-lg text-white mb-2" onclick="showView('dashboard')">
            <span class="text-lg mr-3">📊</span>
            Dashboard
          </button>
          <button class="nav-item w-full text-left px-4 py-3 rounded-lg text-white mb-2" onclick="showView('barangays')">
            <span class="text-lg mr-3">🏘️</span>
            Barangays
          </button>
          <button class="nav-item w-full text-left px-4 py-3 rounded-lg text-white mb-2" onclick="showView('masterlist')">
            <span class="text-lg mr-3">👥</span>
            Community Masterlist
          </button>
          <button class="nav-item w-full text-left px-4 py-3 rounded-lg text-white mb-2" onclick="showView('household')">
            <span class="text-lg mr-3">🏠</span>
            Household Tracking
          </button>
          <button class="nav-item w-full text-left px-4 py-3 rounded-lg text-white mb-2" onclick="showView('tribe')">
            <span class="text-lg mr-3">🌍</span>
            Tribe Distribution
          </button>
        `;
        showView('dashboard');
      } else if (role === 'Chieftain') {
        nav.innerHTML = `
          <button class="nav-item active w-full text-left px-4 py-3 rounded-lg text-white mb-2" onclick="showView('masterlist')">
            <span class="text-lg mr-3">👥</span>
            Community Masterlist
          </button>
          <button class="nav-item w-full text-left px-4 py-3 rounded-lg text-white mb-2" onclick="showView('barangays')">
            <span class="text-lg mr-3">🏘️</span>
            Barangays
          </button>
          <button class="nav-item w-full text-left px-4 py-3 rounded-lg text-white mb-2" onclick="showView('tribe')">
            <span class="text-lg mr-3">🌍</span>
            Tribe Distribution
          </button>
        `;
        showView('masterlist');
      } else if (role === 'Admin') {
        nav.innerHTML = `
          <button class="nav-item active w-full text-left px-4 py-3 rounded-lg text-white mb-2" onclick="showView('admin')">
            <span class="text-lg mr-3">⚙️</span>
            Admin Dashboard
          </button>
          <button class="nav-item w-full text-left px-4 py-3 rounded-lg text-white mb-2" onclick="showView('masterlist')">
            <span class="text-lg mr-3">👥</span>
            View All Members
          </button>
          <button class="nav-item w-full text-left px-4 py-3 rounded-lg text-white mb-2" onclick="showView('barangays')">
            <span class="text-lg mr-3">🏘️</span>
            Barangays
          </button>
        `;
        showView('admin');
      }
    }

    function logout() {
      currentUser = null;
      document.getElementById('mainApp').classList.add('hidden');
      document.getElementById('loginScreen').classList.remove('hidden');
      document.getElementById('loginForm').reset();
      showToast('Logged out successfully', 'success');
    }

    // View Management
    function showView(viewName) {
      const views = ['dashboard', 'barangays', 'masterlist', 'household', 'tribe', 'admin'];
      views.forEach(view => {
        const element = document.getElementById(`${view}View`);
        if (element) {
          element.classList.toggle('hidden', view !== viewName);
        }
      });

      document.querySelectorAll('.nav-item').forEach(item => {
        item.classList.remove('active');
      });
      event.target.closest('.nav-item').classList.add('active');
      
      currentView = viewName;

      // Hide add button for non-IPMR users
      const addBtn = document.getElementById('addMemberBtn');
      if (addBtn) {
        addBtn.classList.toggle('hidden', currentUser.role !== 'IPMR');
      }

      // Update view-specific content
      if (viewName === 'barangays') {
        updateBarangaysView();
      } else if (viewName === 'admin') {
        updateAdminView();
      }
    }

    // Update All Views
    function updateAllViews() {
      updateDashboard();
      updateMembersTable();
      updateHouseholdsView();
      updateTribeView();
      updateFilters();
    }

    // Dashboard Updates
    function updateDashboard() {
      document.getElementById('totalPopulation').textContent = allMembers.length;
      
      const uniqueBarangays = new Set(allMembers.filter(m => m.barangay).map(m => m.barangay));
      document.getElementById('totalBarangays').textContent = uniqueBarangays.size;
      
      const uniqueHouseholds = new Set(allMembers.filter(m => m.householdId).map(m => m.householdId));
      document.getElementById('totalHouseholds').textContent = uniqueHouseholds.size;
      
      const uniqueGroups = new Set(allMembers.filter(m => m.indigenousGroup).map(m => m.indigenousGroup));
      document.getElementById('totalGroups').textContent = uniqueGroups.size;

      const recentActivity = document.getElementById('recentActivities');
      const recent = allMembers.slice(-5).reverse();
      
      if (recent.length === 0) {
        recentActivity.innerHTML = '<p class="text-center py-8 opacity-50">No recent activities</p>';
      } else {
        recentActivity.innerHTML = recent.map(member => `
          <div class="flex items-center justify-between p-4 rounded-lg border hover:bg-gray-50 cursor-pointer" onclick='viewMember("${member.__backendId}")'>
            <div class="flex items-center gap-4">
              ${member.photoData ? `<img src="${member.photoData}" class="w-12 h-12 rounded-full object-cover">` : '<div class="w-12 h-12 rounded-full bg-blue-100 flex items-center justify-center text-xl">👤</div>'}
              <div>
                <div class="font-medium">${member.firstName} ${member.lastName}</div>
                <div class="text-sm opacity-75">${member.barangay || 'No barangay'} • ${member.indigenousGroup || 'No group'}</div>
              </div>
            </div>
            <div class="text-sm opacity-75">${new Date(member.createdAt).toLocaleDateString()}</div>
          </div>
        `).join('');
      }
    }

    // Barangays View
    function updateBarangaysView() {
      const container = document.getElementById('barangaysGrid');
      
      const barangayData = BARANGAYS.map(barangay => {
        const members = allMembers.filter(m => m.barangay === barangay);
        return { name: barangay, count: members.length };
      });

      container.innerHTML = barangayData.map(brgy => `
        <div class="barangay-card bg-white rounded-lg shadow-md p-4" onclick='showBarangayMembers("${brgy.name}")'>
          <div class="flex items-center justify-between mb-2">
            <h3 class="font-bold text-lg">${brgy.name}</h3>
            <span class="text-2xl">🏘️</span>
          </div>
          <div class="text-3xl font-bold text-blue-600 mb-1">${brgy.count}</div>
          <div class="text-sm opacity-75">Members</div>
          <button class="mt-3 text-blue-600 text-sm hover:underline">View Details →</button>
        </div>
      `).join('');
    }

    function showBarangayMembers(barangayName) {
      showView('masterlist');
      document.getElementById('filterBarangay').value = barangayName;
      filterMembers();
    }

    // Members Table
    function updateMembersTable() {
      const tbody = document.getElementById('membersTableBody');
      
      if (allMembers.length === 0) {
        tbody.innerHTML = '<tr><td colspan="13" class="px-6 py-8 text-center opacity-50">No members registered yet</td></tr>';
        return;
      }

      tbody.innerHTML = allMembers.map(member => {
        const age = member.age || calculateAgeFromDate(member.dateOfBirth);
        return `
          <tr class="table-row border-b text-sm">
            <td class="px-4 py-3">
              ${member.photoData ? `<img src="${member.photoData}" class="w-10 h-10 rounded-full object-cover">` : '<div class="w-10 h-10 rounded-full bg-gray-200 flex items-center justify-center text-xs">👤</div>'}
            </td>
            <td class="px-4 py-3 font-medium">${member.lastName}, ${member.firstName} ${member.middleName || ''}</td>
            <td class="px-4 py-3">${age}</td>
            <td class="px-4 py-3">${member.sex}</td>
            <td class="px-4 py-3">${member.civilStatus}</td>
            <td class="px-4 py-3 max-w-xs truncate" title="${member.completeAddress}">${member.completeAddress}</td>
            <td class="px-4 py-3">${member.barangay}</td>
            <td class="px-4 py-3">${member.contactNumber || 'N/A'}</td>
            <td class="px-4 py-3">${member.educationLevel || 'N/A'}</td>
            <td class="px-4 py-3 max-w-xs truncate" title="${member.occupation || 'N/A'}">${member.occupation || 'N/A'}</td>
            <td class="px-4 py-3">${member.indigenousGroup || 'N/A'}</td>
            <td class="px-4 py-3 max-w-xs truncate" title="${member.bloodlinePercentage || 'N/A'}">${member.bloodlinePercentage || 'N/A'}</td>
            <td class="px-4 py-3">
              <div class="flex gap-2">
                <button onclick='viewMember("${member.__backendId}")' class="text-blue-600 hover:underline font-medium text-sm">View</button>
                ${currentUser.role === 'IPMR' ? `
                  <button onclick='editMember("${member.__backendId}")' class="text-green-600 hover:underline font-medium text-sm">Edit</button>
                  <button onclick='deleteMemberFromTable("${member.__backendId}")' class="text-red-600 hover:underline font-medium text-sm">Delete</button>
                ` : ''}
              </div>
            </td>
          </tr>
        `;
      }).join('');
    }

    // Toggle Filter Panel
    function toggleFilterPanel() {
      const panel = document.getElementById('filterPanel');
      panel.classList.toggle('hidden');
    }

    // Clear All Filters
    function clearAllFilters() {
      document.getElementById('searchMembers').value = '';
      document.getElementById('filterBarangay').value = '';
      document.getElementById('filterSex').value = '';
      document.getElementById('filterCivilStatus').value = '';
      document.getElementById('filterGroup').value = '';
      document.getElementById('filterAge').value = '';
      document.getElementById('filterEducation').value = '';
      document.getElementById('filterRelation').value = '';
      document.getElementById('filterReligion').value = '';
      filterMembers();
    }

    // Update Active Filter Count
    function updateFilterCount() {
      let activeCount = 0;
      if (document.getElementById('filterBarangay').value) activeCount++;
      if (document.getElementById('filterSex').value) activeCount++;
      if (document.getElementById('filterCivilStatus').value) activeCount++;
      if (document.getElementById('filterGroup').value) activeCount++;
      if (document.getElementById('filterAge').value) activeCount++;
      if (document.getElementById('filterEducation').value) activeCount++;
      if (document.getElementById('filterRelation').value) activeCount++;
      if (document.getElementById('filterReligion').value) activeCount++;

      const countBadge = document.getElementById('activeFilterCount');
      const clearBtn = document.getElementById('clearFiltersBtn');
      
      if (activeCount > 0) {
        countBadge.textContent = activeCount;
        countBadge.classList.remove('hidden');
        clearBtn.classList.remove('hidden');
      } else {
        countBadge.classList.add('hidden');
        clearBtn.classList.add('hidden');
      }
    }

    // Filter Members
    function filterMembers() {
      const searchTerm = document.getElementById('searchMembers').value.toLowerCase();
      const barangayFilter = document.getElementById('filterBarangay').value;
      const sexFilter = document.getElementById('filterSex').value;
      const civilStatusFilter = document.getElementById('filterCivilStatus').value;
      const groupFilter = document.getElementById('filterGroup').value;
      const ageFilter = document.getElementById('filterAge').value;
      const educationFilter = document.getElementById('filterEducation').value;
      const relationFilter = document.getElementById('filterRelation').value;
      const religionFilter = document.getElementById('filterReligion').value;

      updateFilterCount();

      const filtered = allMembers.filter(member => {
        const fullName = `${member.firstName} ${member.lastName}`.toLowerCase();
        const matchesSearch = fullName.includes(searchTerm);
        const matchesBarangay = !barangayFilter || member.barangay === barangayFilter;
        const matchesSex = !sexFilter || member.sex === sexFilter;
        const matchesCivilStatus = !civilStatusFilter || member.civilStatus === civilStatusFilter;
        const matchesGroup = !groupFilter || member.indigenousGroup === groupFilter;
        
        // Age range filter
        let matchesAge = true;
        if (ageFilter) {
          const age = member.age || calculateAgeFromDate(member.dateOfBirth);
          if (ageFilter === '0-17') matchesAge = age >= 0 && age <= 17;
          else if (ageFilter === '18-35') matchesAge = age >= 18 && age <= 35;
          else if (ageFilter === '36-59') matchesAge = age >= 36 && age <= 59;
          else if (ageFilter === '60+') matchesAge = age >= 60;
        }

        const matchesEducation = !educationFilter || member.educationLevel === educationFilter;
        const matchesRelation = !relationFilter || member.relationToHead === relationFilter;
        const matchesReligion = !religionFilter || member.religion === religionFilter;

        return matchesSearch && matchesBarangay && matchesSex && matchesCivilStatus && 
               matchesGroup && matchesAge && matchesEducation && matchesRelation && matchesReligion;
      });

      const tbody = document.getElementById('membersTableBody');
      if (filtered.length === 0) {
        tbody.innerHTML = '<tr><td colspan="13" class="px-6 py-8 text-center opacity-50">No members match your filters</td></tr>';
        return;
      }

      tbody.innerHTML = filtered.map(member => {
        const age = member.age || calculateAgeFromDate(member.dateOfBirth);
        return `
          <tr class="table-row border-b text-sm">
            <td class="px-4 py-3">
              ${member.photoData ? `<img src="${member.photoData}" class="w-10 h-10 rounded-full object-cover">` : '<div class="w-10 h-10 rounded-full bg-gray-200 flex items-center justify-center text-xs">👤</div>'}
            </td>
            <td class="px-4 py-3 font-medium">${member.lastName}, ${member.firstName} ${member.middleName || ''}</td>
            <td class="px-4 py-3">${age}</td>
            <td class="px-4 py-3">${member.sex}</td>
            <td class="px-4 py-3">${member.civilStatus}</td>
            <td class="px-4 py-3 max-w-xs truncate" title="${member.completeAddress}">${member.completeAddress}</td>
            <td class="px-4 py-3">${member.barangay}</td>
            <td class="px-4 py-3">${member.contactNumber || 'N/A'}</td>
            <td class="px-4 py-3">${member.educationLevel || 'N/A'}</td>
            <td class="px-4 py-3 max-w-xs truncate" title="${member.occupation || 'N/A'}">${member.occupation || 'N/A'}</td>
            <td class="px-4 py-3">${member.indigenousGroup || 'N/A'}</td>
            <td class="px-4 py-3 max-w-xs truncate" title="${member.bloodlinePercentage || 'N/A'}">${member.bloodlinePercentage || 'N/A'}</td>
            <td class="px-4 py-3">
              <div class="flex gap-2">
                <button onclick='viewMember("${member.__backendId}")' class="text-blue-600 hover:underline font-medium text-sm">View</button>
                ${currentUser.role === 'IPMR' ? `
                  <button onclick='editMember("${member.__backendId}")' class="text-green-600 hover:underline font-medium text-sm">Edit</button>
                  <button onclick='deleteMemberFromTable("${member.__backendId}")' class="text-red-600 hover:underline font-medium text-sm">Delete</button>
                ` : ''}
              </div>
            </td>
          </tr>
        `;
      }).join('');
    }

    // Update Filters
    function updateFilters() {
      const barangayFilter = document.getElementById('filterBarangay');
      const groupFilter = document.getElementById('filterGroup');
      const religionFilter = document.getElementById('filterReligion');
      
      const currentBarangay = barangayFilter.value;
      const currentGroup = groupFilter.value;
      const currentReligion = religionFilter.value;

      barangayFilter.innerHTML = '<option value="">All Barangays</option>' + 
        BARANGAYS.map(brgy => `<option value="${brgy}">${brgy}</option>`).join('');
      barangayFilter.value = currentBarangay;

      const ALL_INDIGENOUS_GROUPS = [
        'Aeta', 'Agta', 'Ayta', 'Agta (Cagayan Valley)', 'Dumagat', 'Atta', 'Isneg', 'Ibanag',
        'Itawes', 'Isinay', 'Ilongot (Bugkalot)', 'Remontado', 'Iraya', 'Alangan', 'Tadyawan',
        'Tau-buid', 'Buhid', 'Hanunuo', 'Bangon', 'Ratagnon', 'Bontok', 'Ibaloy', 'Ifugao',
        'Kalinga', 'Kankanaey', 'Tingguian (Itneg)', 'Ikalahan (Kalanguya)', 'Ati', 'Bukidnon',
        'Magahat', 'Ata', 'Bagobo', 'Banwaon', "B'laan", 'Dibabawon', 'Higaonon', 'Manobo',
        'Mamanwa', 'Mandaya', 'Mansaka', 'Subanen', 'Tagakaulo', 'Talaandig', 'Teduray',
        'Ubo / Obu-Manuvu', 'Badjao', 'Maranao', 'Maguindanaon', 'Tausug', 'Sama', 'Yakan'
      ];
      groupFilter.innerHTML = '<option value="">All Indigenous Groups</option>' + 
        ALL_INDIGENOUS_GROUPS.map(group => `<option value="${group}">${group}</option>`).join('');
      groupFilter.value = currentGroup;

      const uniqueReligions = [...new Set(allMembers.filter(m => m.religion).map(m => m.religion))];
      religionFilter.innerHTML = '<option value="">All Religions</option>' + 
        uniqueReligions.map(religion => `<option value="${religion}">${religion}</option>`).join('');
      religionFilter.value = currentReligion;
    }

    // Households View
    function updateHouseholdsView() {
      const container = document.getElementById('householdsContainer');
      const households = {};
      
      allMembers.forEach(member => {
        if (member.householdId) {
          if (!households[member.householdId]) {
            households[member.householdId] = [];
          }
          households[member.householdId].push(member);
        }
      });

      if (Object.keys(households).length === 0) {
        container.innerHTML = '<div class="bg-white rounded-xl shadow-md p-6 text-center opacity-50"><p class="py-8">No households registered yet</p></div>';
        return;
      }

      container.innerHTML = Object.entries(households).map(([householdId, members]) => {
        const head = members.find(m => m.relationToHead === 'Head') || members[0];
        return `
          <div class="bg-white rounded-xl shadow-md p-6 mb-6">
            <div class="flex items-center justify-between mb-6 pb-4 border-b">
              <div>
                <h3 class="text-2xl font-bold">🏠 ${householdId}</h3>
                <p class="text-sm opacity-75 mt-1">Household Head: ${head.firstName} ${head.lastName}</p>
              </div>
              <span class="px-4 py-2 rounded-full text-sm font-medium bg-blue-100 text-blue-800">${members.length} members</span>
            </div>
            
            <div class="flex flex-wrap gap-4 justify-center">
              ${members.map(m => `
                <div class="text-center">
                  ${m.photoData ? `<img src="${m.photoData}" class="w-20 h-20 rounded-full object-cover mx-auto mb-2 border-2 ${m.relationToHead === 'Head' ? 'border-blue-600' : 'border-gray-300'}">` : `<div class="w-20 h-20 rounded-full bg-gray-200 flex items-center justify-center text-2xl mx-auto mb-2 border-2 ${m.relationToHead === 'Head' ? 'border-blue-600' : 'border-gray-300'}">👤</div>`}
                  <div class="font-medium text-sm">${m.firstName}</div>
                  <div class="text-xs opacity-75">${m.relationToHead || 'Member'}</div>
                </div>
              `).join('')}
            </div>
          </div>
        `;
      }).join('');
    }

    // Tribe Distribution View
    function updateTribeView() {
      const tribeChart = document.getElementById('tribeChart');
      const bloodlineChart = document.getElementById('bloodlineChart');

      // Indigenous group distribution
      const groupCounts = {};
      allMembers.forEach(member => {
        const group = member.indigenousGroup || 'Not Specified';
        groupCounts[group] = (groupCounts[group] || 0) + 1;
      });

      if (Object.keys(groupCounts).length === 0 || allMembers.length === 0) {
        tribeChart.innerHTML = '<p class="text-center py-8 opacity-50">No tribe data available</p>';
        bloodlineChart.innerHTML = '<p class="text-center py-8 opacity-50">No bloodline data available</p>';
        return;
      }

      tribeChart.innerHTML = Object.entries(groupCounts).map(([group, count]) => {
        const percentage = ((count / allMembers.length) * 100).toFixed(1);
        return `
          <div>
            <div class="flex justify-between text-sm mb-2">
              <span class="font-medium">${group}</span>
              <span class="font-bold">${count} (${percentage}%)</span>
            </div>
            <div class="w-full bg-gray-200 rounded-full h-3">
              <div class="bg-blue-600 h-3 rounded-full transition-all" style="width: ${percentage}%"></div>
            </div>
          </div>
        `;
      }).join('');

      // Bloodline percentages
      const bloodlineData = allMembers.filter(m => m.bloodlinePercentage);
      if (bloodlineData.length === 0) {
        bloodlineChart.innerHTML = '<p class="text-center py-8 opacity-50">No bloodline data available</p>';
      } else {
        bloodlineChart.innerHTML = bloodlineData.slice(0, 10).map(member => `
          <div class="p-4 border rounded-lg">
            <div class="font-medium mb-2">${member.firstName} ${member.lastName}</div>
            <div class="text-sm opacity-75">${member.bloodlinePercentage}</div>
          </div>
        `).join('');
      }
    }

    // Admin View
    function updateAdminView() {
      document.getElementById('adminTotalUsers').textContent = '3';
      document.getElementById('adminTotalMembers').textContent = allMembers.length;
      document.getElementById('adminDbSize').textContent = Math.round(JSON.stringify(allMembers).length / 1024) + ' KB';

      const loginHistory = document.getElementById('loginHistoryBody');
      loginHistory.innerHTML = `
        <tr class="border-b">
          <td class="px-4 py-3">${currentUser.name}</td>
          <td class="px-4 py-3">${currentUser.role}</td>
          <td class="px-4 py-3">${new Date().toLocaleString()}</td>
          <td class="px-4 py-3"><span class="px-3 py-1 bg-green-100 text-green-800 rounded-full text-sm">Active</span></td>
        </tr>
      `;
    }

    // Photo Functions
    async function startCamera() {
      try {
        cameraStream = await navigator.mediaDevices.getUserMedia({ video: { facingMode: 'user' } });
        const video = document.getElementById('cameraVideo');
        video.srcObject = cameraStream;
        document.getElementById('cameraModal').classList.remove('hidden');
        document.getElementById('cameraModal').classList.add('flex');
      } catch (error) {
        showToast('Camera access denied or not available', 'error');
      }
    }

    function stopCamera() {
      if (cameraStream) {
        cameraStream.getTracks().forEach(track => track.stop());
        cameraStream = null;
      }
      document.getElementById('cameraModal').classList.add('hidden');
      document.getElementById('cameraModal').classList.remove('flex');
    }

    function capturePhoto() {
      const video = document.getElementById('cameraVideo');
      const canvas = document.getElementById('cameraCanvas');
      canvas.width = video.videoWidth;
      canvas.height = video.videoHeight;
      const ctx = canvas.getContext('2d');
      ctx.drawImage(video, 0, 0);
      
      capturedPhotoData = canvas.toDataURL('image/jpeg', 0.8);
      document.getElementById('photoPreview').src = capturedPhotoData;
      document.getElementById('photoPreviewContainer').classList.remove('hidden');
      document.getElementById('clearPhotoBtn').classList.remove('hidden');
      
      stopCamera();
      showToast('Photo captured successfully', 'success');
    }

    function clearPhoto() {
      capturedPhotoData = null;
      document.getElementById('photoPreviewContainer').classList.add('hidden');
      document.getElementById('clearPhotoBtn').classList.add('hidden');
    }

    // Modal Functions
    function openAddMemberModal() {
      document.getElementById('addMemberModal').classList.remove('hidden');
      document.getElementById('addMemberModal').classList.add('flex');
    }

    function closeAddMemberModal() {
      document.getElementById('addMemberModal').classList.add('hidden');
      document.getElementById('addMemberModal').classList.remove('flex');
      document.getElementById('addMemberForm').reset();
      clearPhoto();
      selectedMember = null;
      // Reset modal title and button
      document.querySelector('#addMemberModal .p-6.border-b h3').textContent = 'Add New Community Member';
      document.getElementById('submitMemberBtn').textContent = 'Add Member';
    }

    function calculateAge() {
      const dobInput = document.querySelector('input[name="dateOfBirth"]');
      const ageInput = document.getElementById('ageInput');
      if (dobInput.value) {
        const age = calculateAgeFromDate(dobInput.value);
        ageInput.value = age;
      }
    }

    function calculateBloodline() {
      const motherGroup = document.getElementById('motherGroup').value.trim();
      const fatherGroup = document.getElementById('fatherGroup').value.trim();
      const calculatedDisplay = document.getElementById('calculatedBloodline');
      const bloodlineInput = document.getElementById('bloodlinePercentage');
      const indigenousGroupInput = document.getElementById('indigenousGroup');

      if (!motherGroup && !fatherGroup) {
        calculatedDisplay.textContent = 'Enter parent\'s groups to calculate';
        bloodlineInput.value = '';
        return;
      }

      if (!motherGroup || !fatherGroup) {
        calculatedDisplay.textContent = 'Please enter both parent\'s groups';
        bloodlineInput.value = '';
        return;
      }

      // Calculate 50-50 split from parents
      const bloodlineText = `50% ${motherGroup}, 50% ${fatherGroup}`;
      calculatedDisplay.textContent = bloodlineText;
      bloodlineInput.value = bloodlineText;

      // Auto-fill primary indigenous group if empty
      if (!indigenousGroupInput.value) {
        indigenousGroupInput.value = `${motherGroup}-${fatherGroup}`;
      }
    }

    function calculateAgeFromDate(dateOfBirth) {
      const today = new Date();
      const birthDate = new Date(dateOfBirth);
      let age = today.getFullYear() - birthDate.getFullYear();
      const monthDiff = today.getMonth() - birthDate.getMonth();
      if (monthDiff < 0 || (monthDiff === 0 && today.getDate() < birthDate.getDate())) {
        age--;
      }
      return age;
    }

    // Form Submission
    document.getElementById('addMemberForm').addEventListener('submit', async (e) => {
      e.preventDefault();
      
      const submitBtn = document.getElementById('submitMemberBtn');
      const isEditing = submitBtn.textContent === 'Update Member';

      if (!isEditing && allMembers.length >= 999) {
        showToast('Maximum limit of 999 members reached', 'error');
        return;
      }

      const originalText = submitBtn.textContent;
      submitBtn.disabled = true;
      submitBtn.innerHTML = '<div class="loading-spinner mx-auto"></div>';

      const formData = new FormData(e.target);
      const memberData = {
        id: isEditing ? selectedMember.id : `MEM-${Date.now()}`,
        type: 'member',
        userId: currentUser.email,
        userRole: currentUser.role,
        photoData: capturedPhotoData || '',
        lastName: formData.get('lastName'),
        middleName: formData.get('middleName') || '',
        firstName: formData.get('firstName'),
        age: parseInt(formData.get('age')),
        sex: formData.get('sex'),
        dateOfBirth: formData.get('dateOfBirth'),
        civilStatus: formData.get('civilStatus'),
        nationality: formData.get('nationality'),
        religion: formData.get('religion') || '',
        completeAddress: formData.get('completeAddress'),
        barangay: formData.get('barangay'),
        municipality: formData.get('municipality'),
        province: formData.get('province'),
        zipCode: formData.get('zipCode'),
        contactNumber: formData.get('contactNumber') || '',
        email: formData.get('email') || '',
        educationLevel: formData.get('educationLevel') || '',
        occupation: formData.get('occupation') || '',
        householdId: formData.get('householdId') || '',
        relationToHead: formData.get('relationToHead') || '',
        motherGroup: formData.get('motherGroup') || '',
        fatherGroup: formData.get('fatherGroup') || '',
        indigenousGroup: formData.get('indigenousGroup'),
        bloodlinePercentage: formData.get('bloodlinePercentage') || '',
        languages: formData.get('languages') || '',
        createdAt: isEditing ? selectedMember.createdAt : new Date().toISOString(),
        updatedAt: new Date().toISOString(),
        createdBy: isEditing ? selectedMember.createdBy : currentUser.email
      };

      let result;
      if (isEditing) {
        memberData.__backendId = selectedMember.__backendId;
        result = await window.dataSdk.update(memberData);
      } else {
        result = await window.dataSdk.create(memberData);
      }
      
      submitBtn.disabled = false;
      submitBtn.textContent = originalText;

      if (result.isOk) {
        showToast(isEditing ? 'Member updated successfully!' : 'Member added successfully!', 'success');
        closeAddMemberModal();
        selectedMember = null;
        // Reset modal for next use
        document.querySelector('#addMemberModal .p-6.border-b h3').textContent = 'Add New Community Member';
        document.getElementById('submitMemberBtn').textContent = 'Add Member';
      } else {
        showToast(isEditing ? 'Failed to update member. Please try again.' : 'Failed to add member. Please try again.', 'error');
      }
    });

    // View Member
    function viewMember(backendId) {
      selectedMember = allMembers.find(m => m.__backendId === backendId);
      if (!selectedMember) return;

      const content = document.getElementById('memberDetailsContent');
      const age = selectedMember.age || calculateAgeFromDate(selectedMember.dateOfBirth);
      
      content.innerHTML = `
        <div class="flex flex-col items-center mb-6">
          ${selectedMember.photoData ? `<img src="${selectedMember.photoData}" class="w-32 h-32 rounded-full object-cover border-4 border-blue-600 mb-4">` : '<div class="w-32 h-32 rounded-full bg-gray-200 flex items-center justify-center text-5xl mb-4 border-4 border-blue-600">👤</div>'}
          <h3 class="text-2xl font-bold">${selectedMember.firstName} ${selectedMember.middleName || ''} ${selectedMember.lastName}</h3>
          <p class="text-lg opacity-75">${selectedMember.indigenousGroup || 'Indigenous Community Member'}</p>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
          <div class="bg-gray-50 p-4 rounded-lg">
            <h4 class="font-bold mb-3 text-blue-600">Personal Information</h4>
            <div class="space-y-2 text-sm">
              <div><span class="font-medium">Age:</span> ${age} years old</div>
              <div><span class="font-medium">Date of Birth:</span> ${new Date(selectedMember.dateOfBirth).toLocaleDateString()}</div>
              <div><span class="font-medium">Sex:</span> ${selectedMember.sex}</div>
              <div><span class="font-medium">Civil Status:</span> ${selectedMember.civilStatus}</div>
              <div><span class="font-medium">Nationality:</span> ${selectedMember.nationality}</div>
              <div><span class="font-medium">Religion:</span> ${selectedMember.religion || 'N/A'}</div>
            </div>
          </div>

          <div class="bg-gray-50 p-4 rounded-lg">
            <h4 class="font-bold mb-3 text-blue-600">Contact Information</h4>
            <div class="space-y-2 text-sm">
              <div><span class="font-medium">Address:</span> ${selectedMember.completeAddress}</div>
              <div><span class="font-medium">Barangay:</span> ${selectedMember.barangay}</div>
              <div><span class="font-medium">Municipality:</span> ${selectedMember.municipality}</div>
              <div><span class="font-medium">Province:</span> ${selectedMember.province}</div>
              <div><span class="font-medium">ZIP Code:</span> ${selectedMember.zipCode}</div>
              <div><span class="font-medium">Contact:</span> ${selectedMember.contactNumber || 'N/A'}</div>
              <div><span class="font-medium">Email:</span> ${selectedMember.email || 'N/A'}</div>
            </div>
          </div>

          <div class="bg-gray-50 p-4 rounded-lg">
            <h4 class="font-bold mb-3 text-blue-600">Education & Occupation</h4>
            <div class="space-y-2 text-sm">
              <div><span class="font-medium">Education:</span> ${selectedMember.educationLevel || 'N/A'}</div>
              <div><span class="font-medium">Occupation:</span> ${selectedMember.occupation || 'N/A'}</div>
            </div>
          </div>

          <div class="bg-gray-50 p-4 rounded-lg">
            <h4 class="font-bold mb-3 text-blue-600">Household Information</h4>
            <div class="space-y-2 text-sm">
              <div><span class="font-medium">Household ID:</span> ${selectedMember.householdId || 'N/A'}</div>
              <div><span class="font-medium">Relation:</span> ${selectedMember.relationToHead || 'N/A'}</div>
            </div>
          </div>

          <div class="md:col-span-2 bg-gray-50 p-4 rounded-lg">
            <h4 class="font-bold mb-3 text-blue-600">Cultural Information & Bloodline</h4>
            <div class="space-y-2 text-sm">
              <div><span class="font-medium">Mother's Group:</span> ${selectedMember.motherGroup || 'N/A'}</div>
              <div><span class="font-medium">Father's Group:</span> ${selectedMember.fatherGroup || 'N/A'}</div>
              <div class="pt-2 border-t"><span class="font-medium">Calculated Bloodline:</span> <span class="text-blue-600 font-bold">${selectedMember.bloodlinePercentage || 'N/A'}</span></div>
              <div><span class="font-medium">Primary Indigenous Group:</span> ${selectedMember.indigenousGroup || 'N/A'}</div>
              <div><span class="font-medium">Languages:</span> ${selectedMember.languages || 'N/A'}</div>
            </div>
          </div>

          <div class="md:col-span-2 bg-blue-50 p-4 rounded-lg">
            <h4 class="font-bold mb-3 text-blue-600">Record Information</h4>
            <div class="space-y-2 text-sm">
              <div><span class="font-medium">Created:</span> ${new Date(selectedMember.createdAt).toLocaleString()}</div>
              <div><span class="font-medium">Created By:</span> ${selectedMember.createdBy || 'N/A'}</div>
              <div><span class="font-medium">Last Updated:</span> ${new Date(selectedMember.updatedAt).toLocaleString()}</div>
            </div>
          </div>
        </div>
      `;

      const editBtn = document.getElementById('editMemberBtn');
      const deleteBtn = document.getElementById('deleteMemberBtn');
      
      if (currentUser.role === 'IPMR') {
        editBtn.classList.remove('hidden');
        deleteBtn.classList.remove('hidden');
      } else {
        editBtn.classList.add('hidden');
        deleteBtn.classList.add('hidden');
      }

      document.getElementById('viewMemberModal').classList.remove('hidden');
      document.getElementById('viewMemberModal').classList.add('flex');
    }

    function closeViewMemberModal() {
      document.getElementById('viewMemberModal').classList.add('hidden');
      document.getElementById('viewMemberModal').classList.remove('flex');
      selectedMember = null;
    }

    // Edit Member
    function editMember(backendId) {
      selectedMember = allMembers.find(m => m.__backendId === backendId);
      if (!selectedMember) return;

      // Populate form with existing data
      const form = document.getElementById('addMemberForm');
      form.lastName.value = selectedMember.lastName;
      form.firstName.value = selectedMember.firstName;
      form.middleName.value = selectedMember.middleName || '';
      form.dateOfBirth.value = selectedMember.dateOfBirth;
      form.age.value = selectedMember.age;
      form.sex.value = selectedMember.sex;
      form.civilStatus.value = selectedMember.civilStatus;
      form.nationality.value = selectedMember.nationality;
      form.religion.value = selectedMember.religion || '';
      form.completeAddress.value = selectedMember.completeAddress;
      form.barangay.value = selectedMember.barangay;
      form.municipality.value = selectedMember.municipality;
      form.province.value = selectedMember.province;
      form.zipCode.value = selectedMember.zipCode;
      form.contactNumber.value = selectedMember.contactNumber || '';
      form.email.value = selectedMember.email || '';
      form.educationLevel.value = selectedMember.educationLevel || '';
      form.occupation.value = selectedMember.occupation || '';
      form.householdId.value = selectedMember.householdId || '';
      form.relationToHead.value = selectedMember.relationToHead || '';
      document.getElementById('motherGroup').value = selectedMember.motherGroup || '';
      document.getElementById('fatherGroup').value = selectedMember.fatherGroup || '';
      form.indigenousGroup.value = selectedMember.indigenousGroup;
      form.bloodlinePercentage.value = selectedMember.bloodlinePercentage || '';
      form.languages.value = selectedMember.languages || '';

      if (selectedMember.photoData) {
        capturedPhotoData = selectedMember.photoData;
        document.getElementById('photoPreview').src = capturedPhotoData;
        document.getElementById('photoPreviewContainer').classList.remove('hidden');
        document.getElementById('clearPhotoBtn').classList.remove('hidden');
      }

      // Change modal title and button
      document.querySelector('#addMemberModal .p-6.border-b h3').textContent = 'Edit Community Member';
      document.getElementById('submitMemberBtn').textContent = 'Update Member';
      
      openAddMemberModal();
    }

    // Delete Member from Table
    async function deleteMemberFromTable(backendId) {
      const member = allMembers.find(m => m.__backendId === backendId);
      if (!member) return;

      const deleteBtn = event.target;
      const originalText = deleteBtn.textContent;
      
      if (deleteBtn.textContent === 'Delete') {
        deleteBtn.textContent = 'Confirm?';
        deleteBtn.classList.add('font-bold');
        setTimeout(() => {
          if (deleteBtn.textContent === 'Confirm?') {
            deleteBtn.textContent = originalText;
            deleteBtn.classList.remove('font-bold');
          }
        }, 3000);
        return;
      }

      deleteBtn.disabled = true;
      deleteBtn.textContent = '...';

      const result = await window.dataSdk.delete(member);

      if (result.isOk) {
        showToast('Member deleted successfully', 'success');
      } else {
        showToast('Failed to delete member', 'error');
        deleteBtn.disabled = false;
        deleteBtn.textContent = originalText;
      }
    }

    // Delete Member
    document.getElementById('deleteMemberBtn').addEventListener('click', async () => {
      if (!selectedMember) return;

      const deleteBtn = document.getElementById('deleteMemberBtn');
      const originalText = deleteBtn.textContent;
      
      if (deleteBtn.textContent === 'Delete Member') {
        deleteBtn.textContent = 'Confirm Delete?';
        deleteBtn.style.backgroundColor = '#dc2626';
        setTimeout(() => {
          if (deleteBtn.textContent === 'Confirm Delete?') {
            deleteBtn.textContent = originalText;
            deleteBtn.style.backgroundColor = '#ef4444';
          }
        }, 3000);
        return;
      }

      deleteBtn.disabled = true;
      deleteBtn.innerHTML = '<div class="loading-spinner mx-auto"></div>';

      const result = await window.dataSdk.delete(selectedMember);
      
      deleteBtn.disabled = false;
      deleteBtn.textContent = originalText;
      deleteBtn.style.backgroundColor = '#ef4444';

      if (result.isOk) {
        showToast('Member deleted successfully', 'success');
        closeViewMemberModal();
      } else {
        showToast('Failed to delete member', 'error');
      }
    });

    // Utility Functions
    function showToast(message, type = 'success') {
      const toast = document.createElement('div');
      toast.className = 'toast';
      toast.textContent = message;
      toast.style.backgroundColor = type === 'success' ? '#10b981' : '#ef4444';
      document.body.appendChild(toast);
      
      setTimeout(() => {
        toast.remove();
      }, 3000);
    }

    // Initialize on load
    initializeApp();
  </script>
 <script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'99aa4531e55da8db',t:'MTc2MjQ5MTY2MS4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
