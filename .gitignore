import tkinter as tk
from tkinter import ttk, messagebox
import csv
from datetime import datetime

# Khởi tạo cửa sổ
root = tk.Tk()
root.title("Thông tin nhân viên")

# Hàm lưu dữ liệu vào file CSV
def save_to_csv():
    data = [entry_id.get(), entry_name.get(), combo_unit.get(), entry_dob.get(),
            entry_id_num.get(), entry_issue_date.get(), combo_gender.get()]
    with open("employee_data.csv", "a", newline="", encoding="utf-8") as f:
        writer = csv.writer(f)
        writer.writerow(data)
    messagebox.showinfo("Thông báo", "Dữ liệu đã được lưu thành công!")

# Hàm kiểm tra sinh nhật
def show_today_birthdays():
    today = datetime.now().strftime("%d/%m/%Y")
    birthdays = []
    try:
        with open("employee_data.csv", "r", encoding="utf-8") as f:
            reader = csv.reader(f)
            for row in reader:
                if row[3] == today:  # Cột ngày sinh (index 3)
                    birthdays.append(row[1])  # Lấy tên nhân viên
    except FileNotFoundError:
        pass
    messagebox.showinfo("Sinh nhật hôm nay", "\n".join(birthdays) if birthdays else "Không có nhân viên nào sinh nhật hôm nay.")

# Xuất danh sách nhân viên sắp xếp giảm dần theo tuổi
def export_sorted_employees():
    try:
        with open("employee_data.csv", "r", encoding="utf-8") as f:
            data = sorted(csv.reader(f), key=lambda x: datetime.strptime(x[3], "%d/%m/%Y"), reverse=True)
        with open("sorted_employees.csv", "w", newline="", encoding="utf-8") as f:
            writer = csv.writer(f)
            writer.writerows(data)
        messagebox.showinfo("Xuất file", "Danh sách đã được xuất ra file sorted_employees.csv.")
    except FileNotFoundError:
        messagebox.showerror("Lỗi", "Không tìm thấy dữ liệu để xuất.")

# Giao diện nhập liệu
tk.Label(root, text="Mã:").grid(row=0, column=0)
entry_id = tk.Entry(root)
entry_id.grid(row=0, column=1)

tk.Label(root, text="Tên:").grid(row=1, column=0)
entry_name = tk.Entry(root)
entry_name.grid(row=1, column=1)

tk.Label(root, text="Đơn vị:").grid(row=2, column=0)
combo_unit = ttk.Combobox(root, values=["Phân xưởng quê hàn", "Phòng kỹ thuật"])
combo_unit.grid(row=2, column=1)

tk.Label(root, text="Ngày sinh (DD/MM/YYYY):").grid(row=3, column=0)
entry_dob = tk.Entry(root)
entry_dob.grid(row=3, column=1)

tk.Label(root, text="Số CMND:").grid(row=4, column=0)
entry_id_num = tk.Entry(root)
entry_id_num.grid(row=4, column=1)

tk.Label(root, text="Ngày cấp:").grid(row=5, column=0)
entry_issue_date = tk.Entry(root)
entry_issue_date.grid(row=5, column=1)

tk.Label(root, text="Giới tính:").grid(row=6, column=0)
combo_gender = ttk.Combobox(root, values=["Nam", "Nữ"])
combo_gender.grid(row=6, column=1)

# Các nút chức năng
tk.Button(root, text="Lưu", command=save_to_csv).grid(row=7, column=0)
tk.Button(root, text="Sinh nhật hôm nay", command=show_today_birthdays).grid(row=7, column=1)
tk.Button(root, text="Xuất toàn bộ danh sách", command=export_sorted_employees).grid(row=8, column=0, columnspan=2)

root.mainloop()
