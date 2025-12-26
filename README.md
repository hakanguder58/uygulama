GitHub profilinde hem göze hitap edecek hem de işlevsel duracak bir proje için Python ile yazılmış bir "Makro Besin ve Kalori Hesaplayıcı" hazırladım. Bu tür projeler, veri işleme ve kullanıcı etkileşimi yeteneklerini göstermek için harikadır.

Aşağıdaki kodu fitness_tracker.py adıyla kaydedip GitHub'a yükleyebilirsin.

Proje Kodu: Makro ve Kalori Takip Aracı
Python

import datetime

class FitnessTracker:
    def __init__(self, name, weight, height, age, gender, activity_level):
        self.name = name
        self.weight = weight  # kg
        self.height = height  # cm
        self.age = age
        self.gender = gender
        self.activity_level = activity_level # 1.2 (sedanter) ile 1.9 (çok aktif) arası

    def calculate_bmr(self):
        """Mifflin-St Jeor Denklemi ile Bazal Metabolizma Hızı Hesaplama"""
        if self.gender.lower() == 'erkek':
            return 10 * self.weight + 6.25 * self.height - 5 * self.age + 5
        else:
            return 10 * self.weight + 6.25 * self.height - 5 * self.age - 161

    def daily_calorie_needs(self):
        """Günlük harcanan toplam enerji (TDEE)"""
        return self.calculate_bmr() * self.activity_level

    def get_macros(self, goal='koruma'):
        """Hedefe göre makro besin dağılımı (Protein, Karbonhidrat, Yağ)"""
        tdee = self.daily_calorie_needs()
        
        if goal == 'zayıflama':
            target_calories = tdee - 500
        elif goal == 'kilo_alma':
            target_calories = tdee + 500
        else:
            target_calories = tdee

        # Ortalama sağlıklı dağılım: %30 Protein, %40 Karbonhidrat, %30 Yağ
        protein = (target_calories * 0.30) / 4
        carbs = (target_calories * 0.40) / 4
        fat = (target_calories * 0.30) / 9

        return {
            "Günlük Kalori Hedefi": round(target_calories),
            "Protein (g)": round(protein),
            "Karbonhidrat (g)": round(carbs),
            "Yağ (g)": round(fat)
        }

# Örnek Kullanım
user = FitnessTracker(name="Deniz", weight=80, height=180, age=25, gender="erkek", activity_level=1.55)
print(f"--- {user.name} için Beslenme Planı ---")
plan = user.get_macros(goal='zayıflama')

for key, value in plan.items():
    print(f"{key}: {value}")
