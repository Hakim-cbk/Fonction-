import numpy as np
import matplotlib.pyplot as plt
import sympy as sp

# إعداد المتغير الرمزي
x = sp.symbols('x')

# تعريف الدالة (قم بتغييرها لأي دالة أخرى)
func_expr = sp.sin(x) * sp.exp(-x/5)  # مثال: sin(x) * e^(-x/5)

# اشتقاق الدالة
deriv_expr = sp.diff(func_expr, x)

# تحويل الدوال إلى دوال عددية (للاستخدام مع numpy)
f = sp.lambdify(x, func_expr, modules=["numpy"])
f_prime = sp.lambdify(x, deriv_expr, modules=["numpy"])

# نطاق x للرسم
x_vals = np.linspace(0, 10, 400)
y_vals = f(x_vals)
y_prime_vals = f_prime(x_vals)

# الرسم
plt.figure(figsize=(10, 6))
plt.plot(x_vals, y_vals, label=f'الدالة: ${sp.latex(func_expr)}$')
plt.plot(x_vals, y_prime_vals, label=f'المشتقة: ${sp.latex(deriv_expr)}$', linestyle='--')

# إعدادات الرسم
plt.title('رسم دالة ومشتقتها')
plt.xlabel('x')
plt.ylabel('y')
plt.legend()
plt.grid(True)
plt.show()
