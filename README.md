# Near-field-channel-in-
frequency Sub-THZ_شبیه سازی و تحلیل رفتار کانال Near-Field در فرکانس های Sub-THZ و مقایسه آن با مدل کلاسیک Far-Field
پروژه ی پایانی درس شبکه های مخابراتی
این پروژه مربوط به درس شبکه‌های مخابراتی است
هدف اصلی پروژه بررسی رفتار کانال مخابراتی در فواصل کوتاه است
در فرکانس‌های بسیار بالا، مدل‌های کلاسیک دقت کافی ندارند
به همین دلیل بررسی ناحیه میدان نزدیک اهمیت زیادی دارد

در این پروژه تمرکز اصلی روی باند فرکانسی بسیار بالا قرار دارد
این باند در نسل‌های آینده شبکه‌های مخابراتی کاربرد گسترده‌ای دارد
به دلیل کوتاه بودن طول موج، فاصله فرستنده و گیرنده اهمیت زیادی پیدا می‌کند

در فواصل کوتاه، امواج هنوز به صورت کامل تخت نشده‌اند
به همین دلیل رفتار کانال دارای نوسان‌های شدید است
این ناحیه به عنوان ناحیه میدان نزدیک شناخته می‌شود

در مقابل، در فواصل دورتر ناحیه میدان دور قرار دارد
در میدان دور، کاهش توان به صورت یکنواخت اتفاق می‌افتد
مدل‌های کلاسیک تنها برای این ناحیه معتبر هستند

در این پروژه ابتدا مدل کلاسیک میدان دور شبیه‌سازی شده است
سپس رفتار کانال در ناحیه میدان نزدیک مدل‌سازی شده است
برای نمایش تفاوت این دو ناحیه، نمودارهای مقایسه‌ای رسم شده‌اند

در مدل میدان نزدیک از یک جمله نوسانی استفاده شده است
این جمله نوسانی تغییرات توان دریافتی را نمایش می‌دهد
نتایج نشان می‌دهد که رفتار کانال کاملاً غیر یکنواخت است

برای نزدیک شدن به شرایط واقعی، نویز به سیگنال اضافه شده است
این نویز اثر اختلال‌های محیطی را شبیه‌سازی می‌کند
مقایسه سیگنال تمیز و نویزی در خروجی‌ها نمایش داده شده است

در ادامه یک مدل تجربی برای کانال در نظر گرفته شده است
پارامترهای این مدل با داده‌های شبیه‌سازی‌شده تطبیق داده شده‌اند
این کار باعث ساده‌سازی تحلیل کانال می‌شود

در این پروژه دو نوع پرتو نیز بررسی شده‌اند
پرتوی اول دارای افت توان سریع‌تری است
پرتوی دوم پایداری بیشتری در فواصل کوتاه نشان می‌دهد

نتایج نشان می‌دهد که پرتو پایدارتر برای میدان نزدیک مناسب‌تر است
این موضوع با نتایج مقاله مرجع هم‌خوانی دارد
به همین دلیل انتخاب نوع پرتو در طراحی لینک اهمیت زیادی دارد

برای تحلیل بصری بهتر، از نمایش دوبعدی توان استفاده شده است
در این نمایش، توان دریافتی بر حسب فاصله و زاویه نشان داده شده است
این نمودار به درک بهتر رفتار کانال کمک می‌کند

تمام شبیه‌سازی‌ها به صورت عددی انجام شده‌اند
نتایج به صورت نمودارهای مختلف نمایش داده شده‌اند
هر نمودار یک جنبه از رفتار کانال را نشان می‌دهد

این پروژه نشان می‌دهد که استفاده از مدل میدان دور کافی نیست
در فرکانس‌های بسیار بالا باید میدان نزدیک در نظر گرفته شود
نادیده گرفتن این موضوع باعث خطای طراحی می‌شود

نتایج پروژه با یافته‌های پژوهشی اخیر هم‌راستا هستند
این موضوع اعتبار شبیه‌سازی انجام‌شده را افزایش می‌دهد
پروژه حاضر می‌تواند پایه‌ای برای مطالعات پیشرفته‌تر باشد

در نهایت می‌توان گفت که میدان نزدیک نقش کلیدی دارد
در طراحی لینک‌های کوتاه‌برد آینده باید این ناحیه لحاظ شود
این پروژه دید مناسبی از چالش‌های شبکه‌های آینده ارائه می‌دهد
# =========================================
# Near-Field Channel Modeling for Sub-THz
# Full Version with 5 Plots
# Ready for Jupyter Notebook
# =========================================

import numpy as np
import matplotlib.pyplot as plt
from scipy.constants import c
from scipy.optimize import curve_fit

# -----------------------------------------
# System Parameters
# -----------------------------------------
f = 140e9                # 140 GHz
wavelength = c / f
Pt = 1
d = np.linspace(0.05, 2.0, 300)  # distance in meters

# -----------------------------------------
# Far-Field Model (Friis)
# -----------------------------------------
def friis_model(d, wavelength):
    return (wavelength / (4*np.pi*d))**2

Pr_far = Pt * friis_model(d, wavelength)

# -----------------------------------------
# Near-Field Model
# -----------------------------------------
def near_field_model(d, wavelength):
    return (wavelength / (4*np.pi*d))**2 * (1 + 0.4*np.cos(2*np.pi*d/wavelength))

Pr_near = Pt * near_field_model(d, wavelength)

# -----------------------------------------
# Add Noise to Near-Field
# -----------------------------------------
np.random.seed(0)
noise = 0.05 * np.random.randn(len(d))
Pr_near_noisy = Pr_near * (1 + noise)

# -----------------------------------------
# Empirical Curve Fitting for Near-Field
# -----------------------------------------
def fitted_model(d, a, b):
    return (a/d**2) * (1 + b*np.cos(2*np.pi*d/wavelength))

params, _ = curve_fit(fitted_model, d, Pr_near_noisy)
Pr_fit = fitted_model(d, params[0], params[1])

# =========================================
# PLOT 1: Far-Field vs Near-Field
# =========================================
plt.figure(figsize=(8,5))
plt.plot(d, 10*np.log10(Pr_far), label="Far-Field (Friis)")
plt.plot(d, 10*np.log10(Pr_near), label="Near-Field")
plt.xlabel("Distance (m)")
plt.ylabel("Received Power (dB)")
plt.title("Far-Field vs Near-Field")
plt.legend()
plt.grid(True)
plt.show()

# =========================================
# PLOT 2: Near-Field + Curve Fitting
# =========================================
plt.figure(figsize=(8,5))
plt.plot(d, 10*np.log10(Pr_near_noisy), label="Simulated Near-Field (Noisy)")
plt.plot(d, 10*np.log10(Pr_fit), '--', label="Fitted Model")
plt.xlabel("Distance (m)")
plt.ylabel("Received Power (dB)")
plt.title("Near-Field Channel Modeling with Curve Fitting")
plt.legend()
plt.grid(True)
plt.show()

# =========================================
# PLOT 3: Gaussian Beam vs Bessel Beam
# =========================================
def gaussian_beam(d):
    return Pr_near * np.exp(-d/0.5)  # simplified Gaussian decay

def bessel_beam(d):
    return Pr_near * (1 + 0.2*np.cos(2*np.pi*d/wavelength))  # simplified Bessel effect

Pr_gaussian = gaussian_beam(d)
Pr_bessel = bessel_beam(d)

plt.figure(figsize=(8,5))
plt.plot(d, 10*np.log10(Pr_gaussian), label="Gaussian Beam")
plt.plot(d, 10*np.log10(Pr_bessel), label="Bessel Beam")
plt.xlabel("Distance (m)")
plt.ylabel("Received Power (dB)")
plt.title("Gaussian vs Bessel Beam in Near-Field")
plt.legend()
plt.grid(True)
plt.show()

# =========================================
# PLOT 4: Noise Effect (Near-Field Clean vs Noisy)
# =========================================
plt.figure(figsize=(8,5))
plt.plot(d, 10*np.log10(Pr_near), label="Near-Field Clean")
plt.plot(d, 10*np.log10(Pr_near_noisy), label="Near-Field Noisy")
plt.xlabel("Distance (m)")
plt.ylabel("Received Power (dB)")
plt.title("Effect of Noise on Near-Field Channel")
plt.legend()
plt.grid(True)
plt.show()

# =========================================
# PLOT 5: Heatmap 2D of Received Power
# Distance vs Beam Angle Simulation
# =========================================
angles = np.linspace(-30,30,50)  # beam angle in degrees
D, A = np.meshgrid(d, angles)
Pr_heatmap = (wavelength/(4*np.pi*D))**2 * (1 + 0.3*np.cos(2*np.pi*D/wavelength)) * np.cos(np.radians(A))

plt.figure(figsize=(8,5))
plt.pcolormesh(D, A, 10*np.log10(Pr_heatmap), shading='auto', cmap='viridis')
plt.colorbar(label="Received Power (dB)")
plt.xlabel("Distance (m)")
plt.ylabel("Beam Angle (degrees)")
plt.title("Heatmap of Near-Field Received Power vs Distance and Angle")
plt.show()

# =========================================
# Print Fitted Parameters
# =========================================
print("Fitted Parameters for Empirical Near-Field Model:")
print(f"a = {params[0]:.4e}")
print(f"b = {params[1]:.4f}")
