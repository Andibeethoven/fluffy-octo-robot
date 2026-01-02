SOFTWARE LICENSE AGREEMENT

This Software License Agreement (the "Agreement") is entered into by and between the original creator of the software (the "Author") and any user of the software. By using the software, you agree to the terms of this Agreement.

This Software License Agreement (the "Agreement") is entered into by and between the original creator of the software (the "Author") and any user of the software. By using the software, you agree to the terms of this Agreement.

1. LICENSE GRANT
   The Author grants you, the Licensee, a personal, non-transferable, non-exclusive, and revocable license to use the software solely for personal or commercial purposes as specified by the Author. You may not distribute, sublicense, or sell the software unless explicitly authorized by the Author in writing.

2. INTELLECTUAL PROPERTY RIGHTS
   All rights, title, and interest in and to the software, including all intellectual property rights, are and shall remain the exclusive property of the Author. This includes but is not limited to the code, designs, algorithms, and any associated documentation.

3. RESTRICTIONS
   You, the Licensee, shall not:
   a. Copy, distribute, or modify the software except as expressly authorized by the Author.
   b. Use the software for any illegal or unauthorized purposes.
   c. Reverse-engineer, decompile, or attempt to derive the source code or algorithms of the software unless explicitly permitted by law.
   d. Remove or alter any proprietary notices, labels, or markings included in the software.

4. DISCLAIMER OF WARRANTIES
   The software is provided "as is," without any warranties, express or implied, including but not limited to the implied warranties of merchantability, fitness for a particular purpose, and non-infringement. The Author does not warrant that the software will be error-free or uninterrupted.

5. LIMITATION OF LIABILITY
   In no event shall the Author be liable for any direct, indirect, incidental, special, consequential, or exemplary damages (including, but not limited to, damages for loss of profits, goodwill, or data) arising out of the use or inability to use the software, even if the Author has been advised of the possibility of such damages.

6. TERMINATION
   This license is effective until terminated. The Author may terminate this Agreement at any time if you violate its terms. Upon termination, you must immediately cease all use of the software and destroy any copies in your possession.

7. GOVERNING LAW
   This Agreement shall be governed by and construed in accordance with the laws of Australia Victoria, without regard to its conflict of laws principles.

8. AUTHORIZED USE AND SALE
   Only the Author is authorized to sell or distribute this software. Any unauthorized use, sale, or distribution of the software is strictly prohibited and will be subject to legal action.

9. ENTIRE AGREEMENT
   This Agreement constitutes the entire understanding between the parties concerning the subject matter and supersedes all prior agreements ements.

By using this software, you acknowledge that you have read, understood, and agreed to be bound by the terms of this Agreement.

Name : Travis Johnston as Kate Johnston
Date: 02/01/2026

"""
fuzzy-spork — Hardware Core
Time • Life • Meaning
4D Observer-Time Engine (Golden Ratio Driven)

(c) 2025 Travis Peter Lewis Johnston (as Kate JOHNSTON)
Universal Secure Software License v2.0
CLOSED SYSTEM — NO EXTERNAL ACCESS
"""

import math

# ============================================================
# Constants (hardware-safe)
# ============================================================

PHI = (1.0 + math.sqrt(5.0)) / 2.0        # Golden ratio
INV_PHI = 1.0 / PHI
TWO_PI = 2.0 * math.pi


# ============================================================
# Hyperbolic Algebra (scalar, microprocessor-safe)
# ============================================================

def h_expj(t):
    """Split-complex exponential: exp(jt) = (cosh t, sinh t)"""
    return math.cosh(t), math.sinh(t)

def h_norm(x, y):
    """Hyperbolic norm: x² − y²"""
    return x*x - y*y

def h_boost(x, y, eta):
    """Lorentz-style boost in hyperbolic plane"""
    ce = math.cosh(eta)
    se = math.sinh(eta)
    return ce * x + se * y, se * x + ce * y


# ============================================================
# Metatron / Golden Symmetry (scalar)
# ============================================================

def metatron_symmetry_weight():
    """
    Golden-ratio weighted symmetry scalar.
    Fixed cost, deterministic, hardware-stable.
    """
    base = (1, 2, 3, 5, 8, 13, 21)
    acc = 0.0
    for b in base:
        acc += INV_PHI ** (b % 5)
    return acc / len(base)


METATRON_WEIGHT = metatron_symmetry_weight()


# ============================================================
# 4D Time Engine (Hardware Core)
# ============================================================

def time_life_engine(
    t,
    eta,
    life_phase,
    change_rate
):
    """
    Core computation unit.
    Can be called per-cycle on any CPU, phone, or MCU.

    Inputs are normalized scalars [0..1] or small ranges.
    Outputs are scalar metrics usable by firmware or apps.
    """

    # ---- Time phase (golden-ratio frequency) ----
    omega = TWO_PI * INV_PHI
    hx, hy = h_expj(omega * t)

    # ---- Observer boost ----
    bx, by = h_boost(hx, hy, eta)

    # ---- Perceived time rate ----
    R = math.sqrt(abs(h_norm(bx, by)) + 1e-12)
    R *= METATRON_WEIGHT

    # ---- Life meaning ----
    L = 1.0 / (1.0 + math.exp(-6.0 * (life_phase - 0.5)))
    M = math.tanh(eta * (0.6 * L + 0.4 * (1.0 - L)))
    M = (M + 1.0) * 0.5   # normalize 0..1

    # ---- Coherence under change ----
    jitter = 0.05 * math.sin((eta + change_rate) * PHI)
    C = math.exp(-abs(eta) * (0.5 + 1.2 * change_rate)) + jitter
    C = max(0.0, min(1.0, C))

    # ---- Presence ----
    P = math.tanh(
        2.2 * math.sin(TWO_PI * t)
        * (0.8 * math.cos(math.pi * life_phase) + 0.2)
    )
    P = (P + 1.0) * 0.5

    # ---- Life value ----
    life_value = 0.5 * P + 0.5 * C

    return {
        "perceived_time": R,
        "meaning": M,
        "coherence": C,
        "presence": P,
        "life_value": life_value
    }
