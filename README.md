# macro-clicker-pro-antiCHEAT
hello guys
im a new macro maker and if you dont trush me cek my zip or anything in virus total maybe its will be detecks but microsoft and all of super anti virus is call my program save 
if you dont trush me this is the code for my program
#include <iostream>
#include <windows.h>
#include <random>
#include <chrono>

using namespace std;

random_device rd;
mt19937 chaos_engine(rd());

void ChaosSleep(int target_cps) {
    if (target_cps <= 0) return;
    double base_delay_us = 1000000.0 / target_cps;
    uniform_real_distribution<double> dist(-0.25, 0.35);
    double chaos_modifier = dist(chaos_engine);
    
    long long final_delay_us = static_cast<long long>(base_delay_us + (base_delay_us * chaos_modifier));
    if (final_delay_us < 100) final_delay_us = 100;

    auto start = chrono::high_resolution_clock::now();
    while (true) {
        auto now = chrono::high_resolution_clock::now();
        auto elapsed = chrono::duration_cast<chrono::microseconds>(now - start).count();
        if (elapsed >= final_delay_us) break;
    }
}

void MicroJitterSleep() {
    uniform_int_distribution<int> jitter_dist(150, 950);
    long long jitter_us = jitter_dist(chaos_engine);

    auto start = chrono::high_resolution_clock::now();
    while (true) {
        auto now = chrono::high_resolution_clock::now();
        auto elapsed = chrono::duration_cast<chrono::microseconds>(now - start).count();
        if (elapsed >= jitter_us) break;
    }
}

// FIX: Struktur simulasi keyboard yang lolos blokir Roblox
void PressKeyF() {
    INPUT inputs[2] = {};

    // 1. Tombol F Ditekan (Key Down)
    inputs[0].type = INPUT_KEYBOARD;
    inputs[0].ki.wVk = 0x46; // Tombol F
    inputs[0].ki.wScan = MapVirtualKey(0x46, MAPVK_VK_TO_VSC); // FIX: Scan Code Hardware Nyata
    inputs[0].ki.dwFlags = KEYEVENTF_SCANCODE; // Beritahu OS ini input hardware

    // 2. Tombol F Dilepas (Key Up)
    inputs[1].type = INPUT_KEYBOARD;
    inputs[1].ki.wVk = 0x46;
    inputs[1].ki.wScan = MapVirtualKey(0x46, MAPVK_VK_TO_VSC);
    inputs[1].ki.dwFlags = KEYEVENTF_SCANCODE | KEYEVENTF_KEYUP;

    // Kirim urutan tekan-lepas secara sempurna ke Windows Registry
    SendInput(2, inputs, sizeof(INPUT));
}

int main() {
    cout << "=================================================" << endl;
    cout << "      === MACRO DUAL PRO [CHAOS & UNAPPED VERSION] ===" << endl;
    cout << "   Sistem Klik: DUAL INSTANT (F Keyboard + F Jitter)" << endl;
    cout << "      Sistem Pengacak: CHAOS RANDOMIZER (MAIN GILA)" << endl;
    cout << "  Safety Cap Status: DIHAPUS (UNAPPED)" << endl;
    cout << "=================================================" << endl;

    int cps = 20;
    cout << "   Masukkan Batasan CPS (1 - 1000): ";
    cin >> cps;

    if (cps < 1) cps = 1;
    if (cps > 1000) cps = 1000;

    cout << "\n[Q]  : ON / OFF (Ada Suara Beep)" << endl;
    cout << "[F4] : KELUAR" << endl;
    cout << "-------------------------------------------------" << endl;
    cout << "       [STATUS] MACRO: NONAKTIF (STANDBY)" << endl;

    bool isActive = false;
    bool qPressed = false;

    while (true) {
        if (GetAsyncKeyState(VK_F4) & 0x8000) {
            break;
        }

        if (GetAsyncKeyState(0x51) & 0x8000) { // Tombol Q
            if (!qPressed) {
                isActive = !isActive;
                qPressed = true;
                
                if (isActive) {
                    Beep(800, 200);
                    system("cls");
                    cout << "=================================================" << endl;
                    cout << "      === MACRO DUAL PRO [CHAOS & UNAPPED VERSION] ===" << endl;
                    cout << "     [STATUS] MACRO: AKTIF (CHAOS MODE - UNAPPED)" << endl;
                    cout << "=================================================" << endl;
                } else {
                    Beep(500, 200);
                    system("cls");
                    cout << "=================================================" << endl;
                    cout << "      === MACRO DUAL PRO [CHAOS & UNAPPED VERSION] ===" << endl;
                    cout << "       [STATUS] MACRO: NONAKTIF (STANDBY)" << endl;
                    cout << "=================================================" << endl;
                }
            }
        } else {
            qPressed = false;
        }

        if (isActive) {
            PressKeyF(); // Tembakan F Pertama
            MicroJitterSleep(); // Jeda Chaos Jitter
            PressKeyF(); // Tembakan F Kedua
            ChaosSleep(cps); // Delay utama CPS
        } else {
            Sleep(10);
        }
    }

    system("cls");
    cout << "\n[SYSTEM] Makro ditutup aman. Sampai jumpa!" << endl;
    Sleep(2000);
    return 0;
}
