Kundan Singh

Topic:                       Students Marksheet


import numpy as np
import pandas as pd
import matplotlib.pyplot as plt



data = {
    "Name": ["Aman", "Riya", "Karan", "Supriya"],
    "Math": [78, 88, 67, 91],
    "Science": [85, 79, 72, 89],
    "English": [90, 92, 80, 95],
    "Computer": [88, 81, 75, 93]
}

df = pd.DataFrame(data)


df.to_csv("student_marks.csv", index=False)

print("CSV FILE CREATED SUCCESSFULLY!\n")
print(df)



df = pd.read_csv("student_marks.csv")

print("\nREADING CSV FILE:\n")
print(df)



subjects = ["Math", "Science", "English", "Computer"]


avg_marks = df[subjects].mean()
max_marks = df[subjects].max()
min_marks = df[subjects].min()

print("\nAVERAGE MARKS PER SUBJECT:\n", avg_marks)
print("\nMAXIMUM MARKS PER SUBJECT:\n", max_marks)
print("\nMINIMUM MARKS PER SUBJECT:\n", min_marks)


df["Total"] = df[subjects].sum(axis=1)
df["Percentage"] = (df["Total"] / (len(subjects)*100)) * 100


print("\nTOTAL & PERCENTAGE:\n")
print(df[["Name", "Total", "Percentage"]])



plt.figure(figsize=(9,5))
plt.bar(df["Name"], df["Total"])
plt.title("Total Marks Comparison")
plt.xlabel("Students")
plt.ylabel("Total Marks")
plt.grid(axis='y', linestyle='--', alpha=0.6)
plt.show()


plt.figure(figsize=(9,5))
plt.bar(subjects, avg_marks)
plt.title("Average Marks Per Subject")
plt.xlabel("Subjects")
plt.ylabel("Average Marks")
plt.grid(axis='y', linestyle='--', alpha=0.6)
plt.show()


plt.figure(figsize=(10,5))
for i in range(len(df)):
    plt.plot(subjects, df.loc[i, subjects], marker='o', label=df.loc[i,'Name'])


plt.title("Student Performance Across Subjects")
plt.xlabel("Subjects")
plt.ylabel("Marks")
plt.legend()
plt.grid(True)
plt.show()

index = 0
student_name = df.loc[index, "Name"]

plt.figure(figsize=(7,7))
plt.pie(df.loc[index, subjects], labels=subjects, autopct='%1.1f%%')
plt.title(f"Marks Distribution of {student_name}")
plt.show()
