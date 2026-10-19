<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Bend Bike Shop - Staff Rental Management Portal</title>
  <!-- Tailwind CSS -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- Google Fonts: Inter -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&family=JetBrains+Mono:wght@400;500;600&display=swap" rel="stylesheet">
  <!-- Lucide Icons -->
  <script src="https://unpkg.com/lucide@latest"></script>
  
  <script>
    tailwind.config = {
      darkMode: 'class',
      theme: {
        extend: {
          fontFamily: {
            sans: ['Inter', 'sans-serif'],
            mono: ['JetBrains Mono', 'monospace'],
          },
          colors: {
            forest: {
              50: '#f0fdf4',
              100: '#dcfce7',
              500: '#22c55e',
              600: '#16a34a',
              700: '#15803d',
              800: '#166534',
              900: '#14532d',
            },
            bend: {
              pine: '#1b3b2b',
              terracotta: '#d97736',
              river: '#2563eb',
              bark: '#2c2523'
            }
          }
        }
      }
    }
  </script>
  <style>
    /* Custom subtle styling */
    .custom-scrollbar::-webkit-scrollbar {
      width: 6px;
      height: 6px;
    }
    .custom-scrollbar::-webkit-scrollbar-track {
      background: #f1f5f9;
    }
    .custom-scrollbar::-webkit-scrollbar-thumb {
      background: #cbd5e1;
      border-radius: 4px;
    }
    .custom-scrollbar::-webkit-scrollbar-thumb:hover {
      background: #94a3b8;
    }
    @keyframes pulseSlow {
      0%, 100% { opacity: 1; transform: scale(1); }
      50% { opacity: 0.85; transform: scale(1.02); }
    }
    .pulse-subtle {
      animation: pulseSlow 3s infinite ease-in-out;
    }
  </style>
</head>
<body class="bg-slate-100 text-slate-800 antialiased min-h-screen flex flex-col font-sans selection:bg-emerald-500 selection:text-white">

  <!-- TOP HEADER -->
  <header class="bg-white border-b border-slate-200 sticky top-0 z-30 shadow-xs">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex items-center justify-between h-16">
        
        <!-- Brand & Location -->
        <div class="flex items-center space-x-3">
          <div class="w-10 h-10 rounded-xl bg-gradient-to-br from-emerald-700 to-teal-800 flex items-center justify-center text-white shadow-md shadow-emerald-900/10">
            <i data-lucide="bike" class="w-6 h-6"></i>
          </div>
          <div>
            <div class="flex items-center space-x-2">
              <span class="font-bold text-lg tracking-tight text-slate-900">BEND BIKE SHOP</span>
              <span class="inline-flex items-center px-2 py-0.5 rounded text-xs font-semibold bg-emerald-100 text-emerald-800 border border-emerald-200">
                Staff Portal
              </span>
            </div>
            <p class="text-xs text-slate-500 font-medium flex items-center gap-1">
              <i data-lucide="map-pin" class="w-3 h-3 text-slate-400"></i> Deschutes Station • Terminal #03
            </p>
          </div>
        </div>

        <!-- Portal Navigation Switcher -->
        <div class="hidden md:flex items-center bg-slate-100 p-1 rounded-xl border border-slate-200 text-xs font-semibold">
          <button class="px-3 py-1.5 rounded-lg bg-white text-slate-900 shadow-xs flex items-center gap-1.5 transition">
            <i data-lucide="shield-check" class="w-3.5 h-3.5 text-emerald-600"></i>
            Staff Operations
          </button>
          <button onclick="showToast('Switching to Customer Self-Service Kiosk Simulation')" class="px-3 py-1.5 rounded-lg text-slate-600 hover:text-slate-900 flex items-center gap-1.5 transition">
            <i data-lucide="tablet" class="w-3.5 h-3.5 text-slate-400"></i>
            Customer Kiosk
          </button>
          <button onclick="showToast('Switching to Management & Fleet Analytics Overview')" class="px-3 py-1.5 rounded-lg text-slate-600 hover:text-slate-900 flex items-center gap-1.5 transition">
            <i data-lucide="bar-chart-3" class="w-3.5 h-3.5 text-slate-400"></i>
            Management View
          </button>
        </div>

        <!-- Staff Identity & Clock -->
        <div class="flex items-center space-x-4">
          <div class="text-right hidden sm:block">
            <div class="text-xs font-bold text-slate-900">Marcus Chen</div>
            <div class="text-[11px] text-emerald-700 flex items-center justify-end gap-1 font-medium">
              <span class="w-1.5 h-1.5 rounded-full bg-emerald-500 animate-pulse"></span> Shift Active (2:15 PM)
            </div>
          </div>
          <div class="w-9 h-9 rounded-full bg-slate-200 border-2 border-emerald-600/30 flex items-center justify-center font-bold text-slate-700 text-xs shadow-xs">
            MC
          </div>
        </div>

      </div>
    </div>
  </header>

  <!-- SECONDARY NAV BAR / TABS -->
  <nav class="bg-white border-b border-slate-200">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex space-x-1 sm:space-x-8 overflow-x-auto py-2.5">
        <button class="text-slate-500 hover:text-slate-900 px-3 py-1.5 rounded-lg text-sm font-medium flex items-center gap-2 whitespace-nowrap transition">
          <i data-lucide="layers" class="w-4 h-4"></i>
          Active Rentals (14)
        </button>
        <button class="text-slate-500 hover:text-slate-900 px-3 py-1.5 rounded-lg text-sm font-medium flex items-center gap-2 whitespace-nowrap transition">
          <i data-lucide="log-out" class="w-4 h-4"></i>
          Check-Out / Dispatch
        </button>
        <button class="bg-emerald-50 text-emerald-800 border border-emerald-200 px-3 py-1.5 rounded-lg text-sm font-semibold flex items-center gap-2 whitespace-nowrap shadow-xs">
          <i data-lucide="log-in" class="w-4 h-4 text-emerald-600"></i>
          Bike Return
          <span class="bg-emerald-600 text-white text-[10px] font-bold px-1.5 py-0.2 rounded-full ml-1">Live</span>
        </button>
        <button class="text-slate-500 hover:text-slate-900 px-3 py-1.5 rounded-lg text-sm font-medium flex items-center gap-2 whitespace-nowrap transition">
          <i data-lucide="clipboard-list" class="w-4 h-4"></i>
          Inventory Status
        </button>
        <button class="text-slate-500 hover:text-slate-900 px-3 py-1.5 rounded-lg text-sm font-medium flex items-center gap-2 whitespace-nowrap transition">
          <i data-lucide="wrench" class="w-4 h-4"></i>
          Maintenance & Fleet Logs
        </button>
      </div>
    </div>
  </nav>

  <!-- MAIN CONTENT CONTAINER -->
  <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-6 flex-1 w-full">

    <!-- SEARCH & LOOKUP PANEL -->
    <section class="bg-white rounded-2xl border border-slate-200 p-5 shadow-xs mb-6">
      <div class="flex flex-col md:flex-row md:items-center justify-between gap-4">
        <div>
          <h1 class="text-xl font-bold text-slate-900 flex items-center gap-2">
            <i data-lucide="corner-down-left" class="w-5 h-5 text-emerald-600"></i>
            Customer Bike Return Check-In
          </h1>
          <p class="text-xs text-slate-500 mt-0.5">Lookup customer reservation to perform physical safety inspection and settle account balance.</p>
        </div>

        <!-- Quick Demo Switchers -->
        <div class="flex items-center gap-2 text-xs">
          <span class="text-slate-400 font-medium">Quick load test:</span>
          <button onclick="populateSearch('541-555-0192')" class="px-2.5 py-1 bg-slate-100 hover:bg-slate-200 text-slate-700 font-medium rounded-md transition border border-slate-200">
            541-555-0192 (Alex Rivera)
          </button>
          <button onclick="populateSearch('BND-8842')" class="px-2.5 py-1 bg-slate-100 hover:bg-slate-200 text-slate-700 font-medium rounded-md transition border border-slate-200">
            #BND-8842
          </button>
        </div>
      </div>

      <!-- Search Input Form -->
      <div class="mt-4 flex flex-col sm:flex-row gap-3">
        <div class="relative flex-1">
          <div class="absolute inset-y-0 left-0 pl-3.5 flex items-center pointer-events-none text-slate-400">
            <i data-lucide="search" class="w-4 h-4"></i>
          </div>
          <input 
            type="text" 
            id="searchInput"
            value="541-555-0192" 
            placeholder="Search by customer phone number (e.g. 541-555-0192), name, or rental ID..."
            class="w-full pl-10 pr-24 py-2.5 bg-slate-50 border border-slate-300 rounded-xl text-sm font-medium focus:outline-none focus:ring-2 focus:ring-emerald-500 focus:bg-white text-slate-900 transition"
          >
          <div class="absolute inset-y-0 right-1 flex items-center pr-2">
            <span class="text-[11px] font-mono text-slate-400 bg-white border border-slate-200 px-1.5 py-0.5 rounded">Enter ↵</span>
          </div>
        </div>

        <button 
          id="searchBtn"
          onclick="performSearch()"
          class="bg-emerald-600 hover:bg-emerald-700 text-white px-6 py-2.5 rounded-xl font-semibold text-sm flex items-center justify-center gap-2 shadow-xs transition active:scale-95"
        >
          <i data-lucide="scan" class="w-4 h-4"></i>
          Find Rental
        </button>
      </div>
    </section>

    <!-- ACTIVE RENTAL DETAIL VIEW (Rendered Result) -->
    <div id="rentalDetailsContainer" class="space-y-6">

      <!-- TOP METRIC & GRACE PERIOD NOTIFICATION BANNER -->
      <div class="bg-gradient-to-r from-emerald-900 via-teal-900 to-slate-900 text-white rounded-2xl p-5 shadow-sm border border-emerald-800 relative overflow-hidden">
        <div class="absolute right-0 top-0 translate-x-8 -translate-y-8 w-64 h-64 bg-emerald-500/10 rounded-full blur-2xl pointer-events-none"></div>

        <div class="relative z-10 flex flex-col lg:flex-row lg:items-center justify-between gap-5">
          <div>
            <div class="flex flex-wrap items-center gap-2.5">
              <span class="font-mono text-xs px-2.5 py-1 rounded bg-white/10 backdrop-blur-md text-emerald-300 font-semibold border border-white/10">
                RENTAL #BND-8842
              </span>
              <span class="inline-flex items-center gap-1.5 px-2.5 py-1 rounded-full text-xs font-semibold bg-amber-400/20 text-amber-300 border border-amber-400/30">
                <i data-lucide="clock" class="w-3.5 h-3.5"></i>
                In Return Inspection
              </span>
              <span class="text-xs text-slate-300">Origin: Deschutes Trailhead Kiosk #1</span>
            </div>

            <div class="mt-3 flex flex-wrap items-baseline gap-x-6 gap-y-2">
              <h2 class="text-2xl font-extrabold text-white tracking-tight">Alex Rivera</h2>
              <div class="flex items-center gap-4 text-xs text-slate-300">
                <span class="flex items-center gap-1"><i data-lucide="phone" class="w-3.5 h-3.5 text-emerald-400"></i> (541) 555-0192</span>
                <span class="flex items-center gap-1"><i data-lucide="mail" class="w-3.5 h-3.5 text-emerald-400"></i> alex.rivera@example.com</span>
              </div>
            </div>
          </div>

          <!-- TIME RETURN CALCULATION BADGE -->
          <div class="bg-white/10 backdrop-blur-md rounded-xl p-3.5 border border-white/15 flex items-center gap-4">
            <div class="space-y-0.5">
              <div class="text-[11px] uppercase tracking-wider text-slate-300 font-semibold">Scheduled Due</div>
              <div class="text-sm font-bold text-white font-mono">2:00 PM Today</div>
            </div>
            <div class="h-8 w-px bg-white/20"></div>
            <div class="space-y-0.5">
              <div class="text-[11px] uppercase tracking-wider text-amber-300 font-semibold flex items-center gap-1">
                Actual Return
              </div>
              <div class="text-sm font-bold text-amber-300 font-mono">2:15 PM (+15m)</div>
            </div>
          </div>
        </div>

        <!-- Automated Policy Rule Banner -->
        <div class="mt-4 pt-4 border-t border-white/10 flex flex-col sm:flex-row sm:items-center justify-between gap-3 text-xs">
          <div class="flex items-center gap-2 text-emerald-200">
            <div class="w-5 h-5 rounded-full bg-emerald-500/20 flex items-center justify-center shrink-0 border border-emerald-400/30">
              <i data-lucide="shield-alert" class="w-3.5 h-3.5 text-emerald-300"></i>
            </div>
            <div>
              <span class="font-bold text-white">Automated Policy Rule Applied:</span>
              <span class="text-emerald-100"> 15 minutes overdue is within Bend Bike Shop's standard <strong>30-minute complimentary grace period</strong>.</span>
            </div>
          </div>
          <div class="flex items-center gap-2 font-mono font-semibold bg-emerald-950/60 text-emerald-300 px-3 py-1 rounded-lg border border-emerald-500/30">
            <span>Late Fee: $0.00</span>
            <span class="text-white/40">|</span>
            <span class="text-slate-300 font-sans text-[11px]">Saved $25.00</span>
          </div>
        </div>
      </div>

      <!-- MAIN WORKFLOW GRID: Left Inspection (2 Bikes), Right Billing Summary -->
      <div class="grid grid-cols-1 lg:grid-cols-12 gap-6">

        <!-- LEFT COLUMN: 2 BIKES INSPECTION CHECKLIST (Col 8) -->
        <div class="lg:col-span-8 space-y-6">

          <!-- Section Heading -->
          <div class="flex items-center justify-between">
            <div>
              <h3 class="font-bold text-slate-900 text-base flex items-center gap-2">
                <i data-lucide="clipboard-check" class="w-5 h-5 text-emerald-600"></i>
                Physical Equipment Inspection (2 Units)
              </h3>
              <p class="text-xs text-slate-500">Verify structural integrity, gear safety, and returned accessories.</p>
            </div>
            <button onclick="markAllPassed()" class="text-xs font-semibold text-emerald-700 hover:text-emerald-800 bg-emerald-50 hover:bg-emerald-100 px-3 py-1.5 rounded-lg border border-emerald-200 transition flex items-center gap-1.5">
              <i data-lucide="check-check" class="w-3.5 h-3.5"></i>
              Quick-Pass All Checks
            </button>
          </div>

          <!-- BIKE 1: Mountain Bike -->
          <div class="bg-white rounded-2xl border border-slate-200 p-5 shadow-xs transition hover:border-slate-300">
            <div class="flex flex-col sm:flex-row sm:items-center justify-between pb-4 border-b border-slate-100 gap-3">
              <div class="flex items-center gap-3">
                <div class="w-12 h-12 rounded-xl bg-slate-100 flex items-center justify-center border border-slate-200 text-slate-700">
                  <i data-lucide="mountain-snow" class="w-6 h-6 text-emerald-700"></i>
                </div>
                <div>
                  <div class="flex items-center gap-2">
                    <span class="font-bold text-slate-900 text-sm">Trek Fuel EX 8 Gen 6</span>
                    <span class="font-mono text-[11px] px-2 py-0.5 rounded bg-slate-100 font-bold text-slate-700 border border-slate-200">#MB-104</span>
                  </div>
                  <div class="text-xs text-slate-500">Category: Full Suspension Trail • Color: Matte Dark Olive • Size: L</div>
                </div>
              </div>
              <div class="flex items-center gap-2">
                <span class="text-xs text-slate-500 font-medium">Assigned Helmet:</span>
                <span class="text-xs font-mono font-semibold bg-slate-50 px-2 py-1 rounded border border-slate-200 text-slate-700">HLM-089</span>
              </div>
            </div>

            <!-- Inspection Toggles -->
            <div class="mt-4 grid grid-cols-2 sm:grid-cols-4 gap-3">
              <label class="flex items-center p-3 rounded-xl border border-slate-200 bg-slate-50 cursor-pointer hover:bg-emerald-50/50 transition has-[:checked]:bg-emerald-50 has-[:checked]:border-emerald-300">
                <input type="checkbox" id="b1_frame" checked class="w-4 h-4 text-emerald-600 rounded focus:ring-emerald-500 accent-emerald-600">
                <div class="ml-2.5">
                  <span class="text-xs font-semibold text-slate-900 block">Frame & Fork</span>
                  <span class="text-[10px] text-slate-500">No cracks/dents</span>
                </div>
              </label>

              <label class="flex items-center p-3 rounded-xl border border-slate-200 bg-slate-50 cursor-pointer hover:bg-emerald-50/50 transition has-[:checked]:bg-emerald-50 has-[:checked]:border-emerald-300">
                <input type="checkbox" id="b1_brakes" checked class="w-4 h-4 text-emerald-600 rounded focus:ring-emerald-500 accent-emerald-600">
                <div class="ml-2.5">
                  <span class="text-xs font-semibold text-slate-900 block">Hydraulic Brakes</span>
                  <span class="text-[10px] text-slate-500">Firm pad contact</span>
                </div>
              </label>

              <label class="flex items-center p-3 rounded-xl border border-slate-200 bg-slate-50 cursor-pointer hover:bg-emerald-50/50 transition has-[:checked]:bg-emerald-50 has-[:checked]:border-emerald-300">
                <input type="checkbox" id="b1_tires" checked class="w-4 h-4 text-emerald-600 rounded focus:ring-emerald-500 accent-emerald-600">
                <div class="ml-2.5">
                  <span class="text-xs font-semibold text-slate-900 block">Tires & Wheels</span>
                  <span class="text-[10px] text-slate-500">28 PSI, true rims</span>
                </div>
              </label>

              <label class="flex items-center p-3 rounded-xl border border-slate-200 bg-slate-50 cursor-pointer hover:bg-emerald-50/50 transition has-[:checked]:bg-emerald-50 has-[:checked]:border-emerald-300">
                <input type="checkbox" id="b1_drivetrain" checked class="w-4 h-4 text-emerald-600 rounded focus:ring-emerald-500 accent-emerald-600">
                <div class="ml-2.5">
                  <span class="text-xs font-semibold text-slate-900 block">Drivetrain</span>
                  <span class="text-[10px] text-slate-500">Clean shifting</span>
                </div>
              </label>
            </div>

            <!-- Notes field -->
            <div class="mt-3.5 flex items-center gap-3">
              <div class="relative flex-1">
                <input 
                  type="text" 
                  id="bike1_notes"
                  placeholder="Staff observations for #MB-104 (e.g. minor dust from Phil's Trail, wiped down)..." 
                  value="Phil's Trail ride - minor dust on frame, lubricated chain, all components nominal."
                  class="w-full text-xs bg-slate-50 border border-slate-200 rounded-lg px-3 py-2 text-slate-700 focus:outline-none focus:ring-1 focus:ring-emerald-500 focus:bg-white"
                >
              </div>
              <span class="text-[11px] font-semibold text-emerald-700 bg-emerald-50 px-2.5 py-1.5 rounded-lg border border-emerald-200 shrink-0 flex items-center gap-1">
                <i data-lucide="check" class="w-3.5 h-3.5"></i> Pass Inspection
              </span>
            </div>
          </div>

          <!-- BIKE 2: Electric Bike -->
          <div class="bg-white rounded-2xl border border-slate-200 p-5 shadow-xs transition hover:border-slate-300">
            <div class="flex flex-col sm:flex-row sm:items-center justify-between pb-4 border-b border-slate-100 gap-3">
              <div class="flex items-center gap-3">
                <div class="w-12 h-12 rounded-xl bg-amber-50 flex items-center justify-center border border-amber-200 text-amber-700">
                  <i data-lucide="zap" class="w-6 h-6 text-amber-600"></i>
                </div>
                <div>
                  <div class="flex items-center gap-2">
                    <span class="font-bold text-slate-900 text-sm">Specialized Turbo Vado 4.0 (e-Bike)</span>
                    <span class="font-mono text-[11px] px-2 py-0.5 rounded bg-amber-100 font-bold text-amber-900 border border-amber-200">#EB-208</span>
                  </div>
                  <div class="text-xs text-slate-500">Category: Step-Through E-Commuter • 710Wh Battery • Size: M</div>
                </div>
              </div>
              
              <!-- Battery Level Indicator Slider -->
              <div class="bg-slate-50 border border-slate-200 rounded-xl p-2 px-3 flex items-center gap-3">
                <div class="flex items-center gap-1.5 text-xs font-semibold text-slate-700">
                  <i data-lucide="battery-charging" class="w-4 h-4 text-emerald-600"></i>
                  <span>Return Battery:</span>
                </div>
                <div class="flex items-center gap-2">
                  <input 
                    type="range" 
                    id="batterySlider" 
                    min="10" 
                    max="100" 
                    value="78" 
                    oninput="updateBatteryText(this.value)"
                    class="w-20 accent-emerald-600 cursor-pointer"
                  >
                  <span id="batteryDisplay" class="font-mono text-xs font-bold text-emerald-700 bg-white px-2 py-0.5 rounded border border-slate-200">78%</span>
                </div>
              </div>
            </div>

            <!-- E-Bike Specific Inspection Toggles -->
            <div class="mt-4 grid grid-cols-2 sm:grid-cols-4 gap-3">
              <label class="flex items-center p-3 rounded-xl border border-slate-200 bg-slate-50 cursor-pointer hover:bg-emerald-50/50 transition has-[:checked]:bg-emerald-50 has-[:checked]:border-emerald-300">
                <input type="checkbox" id="b2_motor" checked class="w-4 h-4 text-emerald-600 rounded focus:ring-emerald-500 accent-emerald-600">
                <div class="ml-2.5">
                  <span class="text-xs font-semibold text-slate-900 block">Motor & MasterMind</span>
                  <span class="text-[10px] text-slate-500">Display OK, no error</span>
                </div>
              </label>

              <label class="flex items-center p-3 rounded-xl border border-slate-200 bg-slate-50 cursor-pointer hover:bg-emerald-50/50 transition has-[:checked]:bg-emerald-50 has-[:checked]:border-emerald-300">
                <input type="checkbox" id="b2_lock" checked class="w-4 h-4 text-emerald-600 rounded focus:ring-emerald-500 accent-emerald-600">
                <div class="ml-2.5">
                  <span class="text-xs font-semibold text-slate-900 block">Abus Folding Lock</span>
                  <span class="text-[10px] text-slate-500">Key + lock returned</span>
                </div>
              </label>

              <label class="flex items-center p-3 rounded-xl border border-slate-200 bg-slate-50 cursor-pointer hover:bg-emerald-50/50 transition has-[:checked]:bg-emerald-50 has-[:checked]:border-emerald-300">
                <input type="checkbox" id="b2_helmet" checked class="w-4 h-4 text-emerald-600 rounded focus:ring-emerald-500 accent-emerald-600">
                <div class="ml-2.5">
                  <span class="text-xs font-semibold text-slate-900 block">E-Helmet #HLM-102</span>
                  <span class="text-[10px] text-slate-500">Clean & sanitized</span>
                </div>
              </label>

              <label class="flex items-center p-3 rounded-xl border border-slate-200 bg-slate-50 cursor-pointer hover:bg-emerald-50/50 transition has-[:checked]:bg-emerald-50 has-[:checked]:border-emerald-300">
                <input type="checkbox" id="b2_charger" checked class="w-4 h-4 text-emerald-600 rounded focus:ring-emerald-500 accent-emerald-600">
                <div class="ml-2.5">
                  <span class="text-xs font-semibold text-slate-900 block">Charger Port Cap</span>
                  <span class="text-[10px] text-slate-500">Sealed watertight</span>
                </div>
              </label>
            </div>

            <!-- Notes field -->
            <div class="mt-3.5 flex items-center gap-3">
              <div class="relative flex-1">
                <input 
                  type="text" 
                  id="bike2_notes"
                  placeholder="Staff observations for #EB-208..." 
                  value="Returned with 78% charge. Key turned in. No chassis scratches."
                  class="w-full text-xs bg-slate-50 border border-slate-200 rounded-lg px-3 py-2 text-slate-700 focus:outline-none focus:ring-1 focus:ring-emerald-500 focus:bg-white"
                >
              </div>
              <span class="text-[11px] font-semibold text-emerald-700 bg-emerald-50 px-2.5 py-1.5 rounded-lg border border-emerald-200 shrink-0 flex items-center gap-1">
                <i data-lucide="check" class="w-3.5 h-3.5"></i> Pass Inspection
              </span>
            </div>
          </div>

          <!-- Quick Return Stations Action Row -->
          <div class="p-4 bg-slate-50 rounded-xl border border-slate-200 flex flex-wrap items-center justify-between gap-3 text-xs">
            <div class="flex items-center gap-2 text-slate-600">
              <i data-lucide="sparkles" class="w-4 h-4 text-emerald-600"></i>
              <span>Next destination after return: <strong>Bay 4 (Sanitization & Battery Docking)</strong></span>
            </div>
            <div class="flex items-center gap-2">
              <button onclick="showToast('Maintenance work order created for fleet team')" class="text-slate-600 hover:text-slate-900 font-medium px-2.5 py-1 bg-white border border-slate-200 rounded-md shadow-2xs">
                Flag for Deep Tune-up
              </button>
            </div>
          </div>

        </div>

        <!-- RIGHT COLUMN: FINANCIAL / BILLING SUMMARY & ACTIONS (Col 4) -->
        <div class="lg:col-span-4 space-y-6">

          <!-- Billing Breakdown Card -->
          <div class="bg-white rounded-2xl border border-slate-200 shadow-xs overflow-hidden">
            <div class="p-5 border-b border-slate-100 bg-slate-50/70 flex items-center justify-between">
              <div>
                <h3 class="font-bold text-slate-900 text-sm">Settlement & Charges</h3>
                <p class="text-xs text-slate-500">Hourly reservation reconciliation</p>
              </div>
              <span class="inline-flex items-center px-2 py-0.5 rounded text-[11px] font-mono font-semibold bg-emerald-100 text-emerald-800">
                Pre-authorized
              </span>
            </div>

            <div class="p-5 space-y-4">
              <!-- Itemized costs -->
              <div class="space-y-2.5 text-xs">
                <div class="flex justify-between items-center text-slate-600">
                  <span>3-Hour Rental: Trek Fuel EX (#MB-104)</span>
                  <span class="font-medium text-slate-900">$75.00</span>
                </div>
                <div class="flex justify-between items-center text-slate-600">
                  <span>3-Hour Rental: Turbo Vado (#EB-208)</span>
                  <span class="font-medium text-slate-900">$85.00</span>
                </div>
                <div class="flex justify-between items-center text-slate-600">
                  <span>Helmets & Accessory Pack (2x)</span>
                  <span class="font-medium text-slate-900">Included</span>
                </div>
                <div class="flex justify-between items-center text-slate-600">
                  <span>Deschutes County Rec Surcharge</span>
                  <span class="font-medium text-slate-900">$9.60</span>
                </div>

                <div class="pt-2 border-t border-slate-100 flex justify-between items-center text-slate-600">
                  <span>Pre-Paid at Kiosk (11:00 AM)</span>
                  <span class="font-medium text-emerald-700">-$169.60</span>
                </div>

                <!-- Overdue Grace Period Breakdown -->
                <div class="p-3 bg-emerald-50 rounded-xl border border-emerald-200 space-y-1">
                  <div class="flex justify-between items-center">
                    <span class="font-bold text-emerald-900 text-xs">15 Min Overtime Rate</span>
                    <span class="font-mono font-bold text-emerald-700">$0.00</span>
                  </div>
                  <div class="text-[11px] text-emerald-800 leading-relaxed">
                    Standard $25/hr rate waived under the 30-min return grace buffer policy.
                  </div>
                </div>

                <!-- Damage Assessment Toggle -->
                <div class="flex justify-between items-center text-slate-600 pt-1">
                  <span class="flex items-center gap-1.5">
                    Damage / Missing Gear Fee
                    <button onclick="toggleDamageFee()" class="text-[10px] text-slate-400 hover:text-slate-600 underline">(add note)</button>
                  </span>
                  <span id="damageFeeDisplay" class="font-medium text-slate-900">$0.00</span>
                </div>
              </div>

              <!-- Payment Method on File -->
              <div class="p-3 bg-slate-50 rounded-xl border border-slate-200 flex items-center justify-between">
                <div class="flex items-center gap-2.5">
                  <div class="w-8 h-6 bg-slate-900 text-white rounded font-mono text-[9px] font-bold flex items-center justify-center">
                    VISA
                  </div>
                  <div>
                    <div class="text-xs font-semibold text-slate-900">Visa ending in •••• 4118</div>
                    <div class="text-[10px] text-slate-500">Pre-auth hold: $250.00 will be released</div>
                  </div>
                </div>
                <i data-lucide="check-circle-2" class="w-4 h-4 text-emerald-600"></i>
              </div>

              <!-- Final Balance Due Calculation -->
              <div class="pt-3 border-t border-slate-200">
                <div class="flex justify-between items-baseline">
                  <div>
                    <span class="text-sm font-bold text-slate-900 block">Balance Due Now</span>
                    <span class="text-[11px] text-slate-500">Security deposit release triggered</span>
                  </div>
                  <div class="text-right">
                    <span id="finalDueDisplay" class="text-2xl font-extrabold text-slate-900 font-mono">$0.00</span>
                  </div>
                </div>
              </div>

              <!-- Action Buttons -->
              <div class="pt-2 space-y-2">
                <button 
                  id="completeReturnBtn"
                  onclick="triggerReturnProcess()"
                  class="w-full bg-emerald-600 hover:bg-emerald-700 active:bg-emerald-800 text-white font-bold py-3.5 px-4 rounded-xl shadow-md shadow-emerald-700/20 text-sm flex items-center justify-center gap-2 transition transform active:scale-[0.98]"
                >
                  <i data-lucide="check-circle" class="w-4 h-4"></i>
                  Complete Return & Send Receipt
                </button>

                <div class="grid grid-cols-2 gap-2">
                  <button onclick="showToast('Physical slip routed to counter printer #1')" class="w-full py-2 px-3 rounded-lg border border-slate-300 bg-white hover:bg-slate-50 text-slate-700 font-semibold text-xs flex items-center justify-center gap-1.5 transition">
                    <i data-lucide="printer" class="w-3.5 h-3.5 text-slate-500"></i>
                    Print Paper Slip
                  </button>
                  <button onclick="showToast('Quick note saved to customer profile')" class="w-full py-2 px-3 rounded-lg border border-slate-300 bg-white hover:bg-slate-50 text-slate-700 font-semibold text-xs flex items-center justify-center gap-1.5 transition">
                    <i data-lucide="message-square" class="w-3.5 h-3.5 text-slate-500"></i>
                    Add Shift Note
                  </button>
                </div>
              </div>

            </div>

            <!-- Shop Policy Reminder Footer -->
            <div class="bg-slate-50 px-5 py-3 border-t border-slate-200 text-[11px] text-slate-500 flex items-center gap-2">
              <i data-lucide="info" class="w-3.5 h-3.5 text-slate-400 shrink-0"></i>
              <span>Customer is automatically unassigned from fleet telemetry upon confirmation.</span>
            </div>
          </div>

          <!-- Quick Assistance Card -->
          <div class="bg-amber-50/60 rounded-2xl border border-amber-200/80 p-4">
            <div class="flex items-start gap-3">
              <div class="w-7 h-7 rounded-lg bg-amber-100 flex items-center justify-center text-amber-700 shrink-0 font-bold">
                <i data-lucide="life-buoy" class="w-4 h-4"></i>
              </div>
              <div class="text-xs">
                <span class="font-bold text-amber-900 block">Trailhead Help Desk</span>
                <span class="text-amber-800">Customer reported great trail conditions at Phil's Trailhead. Offered 10% coupon for next visit.</span>
              </div>
            </div>
          </div>

        </div>

      </div>

    </div>

  </main>

  <!-- SUCCESS COMPLETION & DIGITAL RECEIPT MODAL -->
  <div id="receiptModal" class="fixed inset-0 z-50 bg-slate-900/60 backdrop-blur-sm hidden items-center justify-center p-4">
    <div class="bg-white rounded-3xl max-w-lg w-full border border-slate-200 shadow-2xl overflow-hidden transform transition-all scale-95 opacity-0 duration-200" id="modalBox">
      
      <!-- Modal Header -->
      <div class="bg-gradient-to-r from-emerald-800 to-teal-800 p-6 text-white text-center relative">
        <button onclick="closeModal()" class="absolute top-4 right-4 text-white/70 hover:text-white bg-white/10 hover:bg-white/20 p-1.5 rounded-full transition">
          <i data-lucide="x" class="w-4 h-4"></i>
        </button>

        <div class="w-14 h-14 bg-white text-emerald-700 rounded-2xl mx-auto flex items-center justify-center shadow-lg mb-3">
          <i data-lucide="badge-check" class="w-8 h-8 stroke-[2.5]"></i>
        </div>

        <h3 class="text-xl font-bold">Return Completed Successfully</h3>
        <p class="text-emerald-100 text-xs mt-1">Rental Agreement #BND-8842 has been closed and settled.</p>
      </div>

      <!-- Receipt Content Body -->
      <div class="p-6 space-y-5">
        
        <!-- Delivery Badge Notification -->
        <div class="bg-emerald-50 border border-emerald-200 rounded-xl p-3 flex items-center gap-3">
          <div class="w-8 h-8 rounded-lg bg-emerald-100 text-emerald-700 flex items-center justify-center shrink-0">
            <i data-lucide="send" class="w-4 h-4"></i>
          </div>
          <div class="text-xs">
            <span class="font-bold text-emerald-900 block">Digital Receipt Dispatched</span>
            <span class="text-emerald-700">SMS sent to <strong>(541) 555-0192</strong> & email to <strong>alex.rivera@example.com</strong></span>
          </div>
        </div>

        <!-- Receipt Details Box -->
        <div class="bg-slate-50 rounded-2xl p-4 border border-slate-200 space-y-3 font-mono text-xs">
          <div class="flex justify-between pb-2 border-b border-slate-200">
            <span class="text-slate-500">Transaction ID:</span>
            <span class="font-semibold text-slate-800">TXN-9982-BND</span>
          </div>
          <div class="flex justify-between pb-2 border-b border-slate-200">
            <span class="text-slate-500">Timestamp:</span>
            <span class="font-semibold text-slate-800" id="receiptTimestamp">Today, 2:15 PM</span>
          </div>
          <div class="flex justify-between pb-2 border-b border-slate-200">
            <span class="text-slate-500">Customer:</span>
            <span class="font-semibold text-slate-800">Alex Rivera</span>
          </div>
          <div class="flex justify-between pb-2 border-b border-slate-200">
            <span class="text-slate-500">Units Checked-In:</span>
            <span class="font-semibold text-slate-800">2 Bikes (#MB-104, #EB-208)</span>
          </div>
          <div class="flex justify-between pb-2 border-b border-slate-200">
            <span class="text-slate-500">Grace Period Applied:</span>
            <span class="font-semibold text-emerald-600">Yes (+15 min / $0 Fee)</span>
          </div>
          <div class="flex justify-between pt-1 text-sm font-bold">
            <span class="text-slate-800 font-sans">Total Additional Charged:</span>
            <span class="text-emerald-700 font-mono">$0.00</span>
          </div>
          <div class="flex justify-between text-[11px] text-slate-500 pt-1">
            <span>Card on File:</span>
            <span>Visa •••• 4118 ($250 Deposit Released)</span>
          </div>
        </div>

        <!-- Fleet Status Update Alert -->
        <div class="p-3 bg-slate-100 rounded-xl text-slate-600 text-xs flex items-center justify-between">
          <div class="flex items-center gap-2">
            <i data-lucide="repeat" class="w-4 h-4 text-slate-500"></i>
            <span>Fleet Status: <strong>Marked as Pending Sanitization</strong></span>
          </div>
          <span class="text-[10px] font-mono font-bold bg-white px-2 py-0.5 rounded border border-slate-300">Bay #4</span>
        </div>

        <!-- Modal Actions -->
        <div class="flex items-center gap-3 pt-2">
          <button onclick="printMockReceipt()" class="flex-1 py-3 px-4 border border-slate-300 hover:bg-slate-50 text-slate-700 font-semibold text-xs rounded-xl flex items-center justify-center gap-2 transition">
            <i data-lucide="printer" class="w-4 h-4"></i>
            Print Receipt Copy
          </button>
          <button onclick="startNewReturn()" class="flex-1 py-3 px-4 bg-emerald-600 hover:bg-emerald-700 text-white font-semibold text-xs rounded-xl flex items-center justify-center gap-2 shadow-xs transition">
            <i data-lucide="plus" class="w-4 h-4"></i>
            Process Next Return
          </button>
        </div>

      </div>

    </div>
  </div>

  <!-- TOAST NOTIFICATION CONTAINER -->
  <div id="toast" class="fixed bottom-5 right-5 z-50 bg-slate-900 text-white px-4 py-3 rounded-xl shadow-lg border border-slate-800 text-xs font-medium flex items-center gap-2.5 transform translate-y-16 opacity-0 transition-all duration-300 pointer-events-none">
    <i data-lucide="bell" class="w-4 h-4 text-emerald-400"></i>
    <span id="toastMessage">Notification message</span>
  </div>

  <!-- SCRIPT LOGIC -->
  <script>
    // Initialize Lucide Icons
    window.addEventListener('DOMContentLoaded', () => {
      lucide.createIcons();
    });

    // Toast utility
    let toastTimeout;
    function showToast(message) {
      const toast = document.getElementById('toast');
      const toastMessage = document.getElementById('toastMessage');
      toastMessage.innerText = message;
      
      toast.classList.remove('translate-y-16', 'opacity-0');
      toast.classList.add('translate-y-0', 'opacity-100');

      clearTimeout(toastTimeout);
      toastTimeout = setTimeout(() => {
        toast.classList.add('translate-y-16', 'opacity-0');
        toast.classList.remove('translate-y-0', 'opacity-100');
      }, 3200);
    }

    // Populate search bar via test chips
    function populateSearch(query) {
      const input = document.getElementById('searchInput');
      input.value = query;
      showToast(`Loaded query: "${query}"`);
      performSearch();
    }

    // Search simulation
    function performSearch() {
      const query = document.getElementById('searchInput').value.trim();
      const container = document.getElementById('rentalDetailsContainer');
      const searchBtn = document.getElementById('searchBtn');

      if (!query) {
        showToast('Please enter a phone number or rental ID');
        return;
      }

      // Show temporary loading state on button
      searchBtn.innerHTML = `<span class="animate-spin inline-block w-4 h-4 border-2 border-white border-t-transparent rounded-full mr-2"></span>Searching...`;
      searchBtn.disabled = true;

      setTimeout(() => {
        searchBtn.innerHTML = `<i data-lucide="scan" class="w-4 h-4 mr-1"></i> Find Rental`;
        searchBtn.disabled = false;
        container.classList.remove('opacity-40');
        showToast(`Found active reservation for Alex Rivera (${query})`);
        lucide.createIcons();
      }, 400);
    }

    // Handle battery slider update
    function updateBatteryText(val) {
      document.getElementById('batteryDisplay').innerText = val + '%';
    }

    // Pass all checklist toggles
    function markAllPassed() {
      const checkboxes = document.querySelectorAll('#rentalDetailsContainer input[type="checkbox"]');
      checkboxes.forEach(cb => cb.checked = true);
      showToast('All safety checks marked as PASSED');
    }

    // Toggle Damage Assessment simulation
    let damageApplied = false;
    function toggleDamageFee() {
      const damageDisplay = document.getElementById('damageFeeDisplay');
      const finalDue = document.getElementById('finalDueDisplay');
      
      if (!damageApplied) {
        damageApplied = true;
        damageDisplay.innerText = '$35.00';
        damageDisplay.classList.add('text-rose-600', 'font-bold');
        finalDue.innerText = '$35.00';
        finalDue.classList.add('text-rose-600');
        showToast('Added $35.00 cleaning / tire repair fee');
      } else {
        damageApplied = false;
        damageDisplay.innerText = '$0.00';
        damageDisplay.classList.remove('text-rose-600', 'font-bold');
        finalDue.innerText = '$0.00';
        finalDue.classList.remove('text-rose-600');
        showToast('Damage fee cleared: standard return');
      }
    }

    // Process Complete Return Trigger
    function triggerReturnProcess() {
      const btn = document.getElementById('completeReturnBtn');
      btn.innerHTML = `<span class="animate-spin inline-block w-4 h-4 border-2 border-white border-t-transparent rounded-full mr-2"></span> Settle & Finalize...`;
      btn.disabled = true;

      setTimeout(() => {
        btn.innerHTML = `<i data-lucide="check-circle" class="w-4 h-4 mr-1.5"></i> Complete Return & Send Receipt`;
        btn.disabled = false;
        openModal();
      }, 700);
    }

    // Open Modal with animation
    function openModal() {
      const modal = document.getElementById('receiptModal');
      const modalBox = document.getElementById('modalBox');
      
      modal.classList.remove('hidden');
      modal.classList.add('flex');

      setTimeout(() => {
        modalBox.classList.remove('scale-95', 'opacity-0');
        modalBox.classList.add('scale-100', 'opacity-100');
      }, 20);

      // Set timestamp
      const now = new Date();
      document.getElementById('receiptTimestamp').innerText = `Today, ${now.toLocaleTimeString([], {hour: '2-digit', minute:'2-digit'})}`;
      lucide.createIcons();
    }

    // Close Modal
    function closeModal() {
      const modal = document.getElementById('receiptModal');
      const modalBox = document.getElementById('modalBox');

      modalBox.classList.remove('scale-100', 'opacity-100');
      modalBox.classList.add('scale-95', 'opacity-0');

      setTimeout(() => {
        modal.classList.add('hidden');
        modal.classList.remove('flex');
      }, 200);
    }

    // Start New Return reset
    function startNewReturn() {
      closeModal();
      document.getElementById('searchInput').value = '';
      showToast('Ready for next return check-in');
    }

    // Mock print receipt
    function printMockReceipt() {
      showToast('Sending receipt to thermal receipt printer...');
    }

    // Allow Enter key to trigger search
    document.getElementById('searchInput').addEventListener('keyup', (e) => {
      if (e.key === 'Enter') {
        performSearch();
      }
    });
  </script>
</body>
</html>
