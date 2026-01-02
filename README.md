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
