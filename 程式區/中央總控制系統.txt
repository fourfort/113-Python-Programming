import random
import matplotlib.pyplot as plt
import numpy as np
class SolarPowerPlant:# 太陽能發電站類，包括能量生產、提取等方法和屬性
    
    def __init__(self, solar_panel_count, efficiency):
        self.solar_panel_count = solar_panel_count
        self.efficiency = efficiency
        self.total_energy_produced = 0
        self.available_energy = 0
        self.total_energy_extracted = 0
        self.hourly_energy_production = []

    def generate_energy(self, hours_of_sunshine):
        self.hourly_energy_production = []
        for hour in range(hours_of_sunshine):
            # 添加隨機因素模擬能量產出的波動
            random_factor = random.uniform(0.8, 1.2)
            # 使用sin函數模擬能量產出的波動
            sin_factor = 0.5 * np.sin(hour * (2 * np.pi / 24)) + 1
            energy_per_panel = self.efficiency * random_factor * sin_factor
            total_hourly_energy = energy_per_panel * self.solar_panel_count
            self.total_energy_produced += total_hourly_energy
            self.hourly_energy_production.append(total_hourly_energy)

    # 獲取總發電量
    def get_total_energy_produced(self):
        return self.total_energy_produced

    def get_hourly_energy_production(self):
        return self.hourly_energy_production

    
    def extract_energy(self, amount):
        max_extraction = self.total_energy_produced * 0.6
        if amount <= max_extraction and amount <= self.total_energy_produced:
            self.total_energy_produced -= amount
            self.available_energy += amount
            self.total_energy_extracted += amount
            print(f"成功提取 {amount} kw能量。")
            # 更新提取能量後的能量產生列表
            extraction_index = len(self.hourly_energy_production) - 1
            self.hourly_energy_production[extraction_index] -= amount
        elif amount > max_extraction:
            print("電量提取失敗：提取的電量超過總發電量的60%。")
        else:
            print("能量提取失敗：提取的能量超過總發電量。")
        print(f"剩餘電量: {self.total_energy_produced} kw")

    def get_total_energy_extracted(self):
        return self.total_energy_extracted
class WindPowerPlant:# 風能發電站類，包括能量生產、提取等方法和屬性
    
    def __init__(self, turbine_count, efficiency):
        self.turbine_count = turbine_count
        self.efficiency = efficiency
        self.total_energy_produced = 0
        self.available_energy = 0
        self.total_energy_extracted = 0
        self.hourly_energy_production = []

    def generate_energy(self, hours_of_wind):
        self.hourly_energy_production = []
        for hour in range(hours_of_wind):
            # 使用弦波函數模擬能量產出的波動
            sin_factor = 0.5 * np.sin(hour * (2 * np.pi / 24)) + 1
            energy_per_turbine = self.efficiency * sin_factor
            total_hourly_energy = energy_per_turbine * self.turbine_count
            self.total_energy_produced += total_hourly_energy
            self.hourly_energy_production.append(total_hourly_energy)

    # 獲取總發電量
    def get_total_energy_produced(self):
        return self.total_energy_produced

    def get_hourly_energy_production(self):
        return self.hourly_energy_production

    def extract_energy(self, amount):
        max_extraction = self.total_energy_produced * 0.6
        if amount <= max_extraction and amount <= self.total_energy_produced:
            self.total_energy_produced -= amount
            self.available_energy += amount
            self.total_energy_extracted += amount
            print(f"成功提取 {amount} kw能量。")
            # 更新提取能量後的能量產生列表
            extraction_index = len(self.hourly_energy_production) - 1
            self.hourly_energy_production[extraction_index] -= amount
        elif amount > max_extraction:
            print("電量提取失敗：提取的電量超過總發電量的60%。")
        else:
            print("能量提取失敗：提取的能量超過總發電量。")
        print(f"剩餘電量: {self.total_energy_produced} kw")

    def get_total_energy_extracted(self):
        return self.total_energy_extracted
class NuclearPowerPlant:# 核能發電站類，包括能量生產、提取等方法和屬性
    
    def __init__(self, reactor_count, efficiency):
        self.reactor_count = reactor_count
        self.efficiency = efficiency
        self.total_energy_produced = 0
        self.available_energy = 0
        self.total_energy_extracted = 0
        self.hourly_energy_production = []

    def generate_energy(self, hours_of_operation):
        self.hourly_energy_production = []
        for hour in range(hours_of_operation):
            random_factor = random.uniform(0.8, 1.2)
            energy_per_reactor = self.efficiency * random_factor
            total_hourly_energy = energy_per_reactor * self.reactor_count
            self.total_energy_produced += total_hourly_energy
            self.hourly_energy_production.append(total_hourly_energy)

    def get_total_energy_produced(self):
        return self.total_energy_produced

    def get_hourly_energy_production(self):
        return self.hourly_energy_production

    def extract_energy(self, amount):
        max_extraction = self.total_energy_produced * 0.6
        if amount <= max_extraction and amount <= self.total_energy_produced:
            self.total_energy_produced -= amount
            self.available_energy += amount
            self.total_energy_extracted += amount
            print(f"成功提取 {amount} kw 能量。")
            extraction_index = len(self.hourly_energy_production) - 1
            self.hourly_energy_production[extraction_index] -= amount
        elif amount > max_extraction:
            print("電量提取失敗：提取的電量超過總發電量的60%。")
        else:
            print("能量提取失敗：提取的能量超過總發電量。")
        print(f"剩餘電量: {self.total_energy_produced} kw")

    def get_total_energy_extracted(self):
        return self.total_energy_extracted
    pass
def welcome_message():# 歡迎消息
    
    print("歡迎使用NIU多能源發電站系統！")
    print("本系統包括太陽能、風能和核能三個發電站。")
    print("您可以透過本系統進行各種操作，包括查詢電量、調度電力以及獲取各站的內部狀況。")
def select_service(): # 用戶選擇服務（查詢、調度、狀態）
   
    print("請選擇需要使用的服務：")
    print("1. 查詢目前儲存電量")
    print("2. 調度電力")
    print("3. 關於各站的內部狀況")
    
    while True:
        choice = input("請問您想選哪一個(請填1,2,3):").strip()
        if choice in ['1', '2', '3']:
            return int(choice)
        else:
            print("啊呦這位同仁，您輸錯了啦~(要填1,2,3)!")
def query_energy(): # 查詢當前儲存電量
   
    print("請選擇要查詢的發電站數量：")
    print("1. 一個")
    print("2. 兩個")
    print("3. 三個")

    station_count = int(input("請選擇您所想查詢的發電站數量："))
    if station_count == 1:
        print("請選擇要查詢的發電站，以下是各發電站的編號：")
        print("1. 太陽能")
        print("2. 風能")
        print("3. 核能")
        station_choice = int(input("那請您選擇發電站的編號："))
        
        if station_choice == 1:
            # 調用太陽能發電站的程式進行運作
            energy = query_solar_energy()
            print(f"太陽能發電站目前儲存的電量為：{energy} kw")
        elif station_choice == 2:
            # 調用風能發電站的程式進行運作
            energy = query_wind_energy()
            print(f"風能發電站目前儲存的電量為：{energy} kw")
        elif station_choice == 3:
            # 調用核能發電站的程式進行運作
            energy = query_nuclear_energy()
            print(f"核能發電站目前儲存的電量為：{energy} kw")
        else:
            print("請輸入有效的發電站編號。")
    elif station_count == 2:
       print("請選擇要查詢的兩個發電站：")
       print("1. 太陽能")
       print("2. 風能")
       print("3. 核能")
       selected_stations = input("請輸入選擇的兩個發電站編號（用空格分開）：").split()
    
       if len(selected_stations) != 2 or not all(station in ['1', '2', '3'] for station in selected_stations):
         print("請輸入有效的發電站編號。")
         return
    
       energy = 0
       for station in selected_stations:
         if station == '1':
            solar_energy = query_solar_energy()
            energy += solar_energy
            print(f"太陽能發電站目前儲存的電量為：{solar_energy} kw")
         elif station == '2':
            wind_energy = query_wind_energy()
            energy += wind_energy
            print(f"風能發電站目前儲存的電量為：{wind_energy} kw")
         elif station == '3':
            nuclear_energy = query_nuclear_energy()
            energy += nuclear_energy
            print(f"核能發電站目前儲存的電量為：{nuclear_energy} kw")
    
       print(f"選擇的兩個發電站目前總共儲存的電量為：{energy} kw")

    
    elif station_count == 3:
        solar_energy = query_solar_energy()
        wind_energy = query_wind_energy()
        nuclear_energy = query_nuclear_energy()
        
        print(f"太陽能發電站目前儲存的電量為：{solar_energy} kw")
        print(f"風能發電站目前儲存的電量為：{wind_energy} kw")
        print(f"核能發電站目前儲存的電量為：{nuclear_energy} kw")
        
        total_energy = solar_energy + wind_energy + nuclear_energy
        print(f"所有三個發電站目前總共儲存的電量為：{total_energy} kw")
    else:
        print("請輸入有效的發電站數量哦~")

    print("這邊就結束查詢完咯~")
def query_solar_energy():  # 調用太陽能發電站程式，返回電量
  
    default_solar_panel_count = 20
    max_module_power = 5000
    module_area = 1.6
    solar_irradiance = 1000

    efficiency = round((max_module_power / module_area) / solar_irradiance * 100, 3)

    print("歡迎使用NPUST太陽能發電站模擬系統！")
    print(f"目前有 {default_solar_panel_count} 台太陽能電池板，每塊效率為 {efficiency} kw。")

    while True:
        know_sunshine_hours = input("是否知道今天的太陽照射時間？(是/否) ").strip().lower()
        if know_sunshine_hours == "是":
            hours_of_sunshine = int(input("請輸入太陽照射時間（小時）："))
            break
        elif know_sunshine_hours == "否":
            weather_condition = input("今天是晴天、陰天還是雨天？ ").strip().lower()
            weather_mapping = {"晴天": 10, "陰天": 5, "雨天": 2}
            hours_of_sunshine = weather_mapping.get(weather_condition, 0)
            if hours_of_sunshine:
                break
            else:
                print("無法識別的天氣狀況，請重新輸入。")

    simulation_count = int(input("請輸入要模擬的次數："))
    total_energy_produced_all_simulations = 0
    hourly_energy_production_all_simulations = [[] for _ in range(simulation_count)]

    for i in range(simulation_count):
        print(f"太陽能發電模擬第{i+1}次開始...")
        solar_plant = SolarPowerPlant(default_solar_panel_count, efficiency)
        solar_plant.generate_energy(hours_of_sunshine)
        hourly_energy_production = solar_plant.get_hourly_energy_production()
        total_energy_produced_all_simulations += sum(hourly_energy_production)
        hourly_energy_production_all_simulations[i] = hourly_energy_production
        print(f"太陽能發電模擬第{i+1}次結束。")  
    print("感謝您參與本次太陽能發電站的操作！祝您一路順風~") 
    return solar_plant.get_total_energy_produced()  
def query_wind_energy():   # 調用風能發電站程式，返回電量
    
    default_turbine_count = 5
    max_turbine_power = 2000
    turbine_blade_length = 15  # 假設風力發電機的葉片長度為15米
    speed_Max = 61.2
    speed_Min = 0


    month_wind_speeds = {
        7: (8, 12),   # 夏季風速快
        8: (8, 12),   # 夏季風速快
        9: (8, 12),   # 夏季風速快
        10: (8, 12),  # 夏季風速快
        11: (5, 8),   # 冬季風速中等
        12: (5, 8),   # 冬季風速中等
        1: (5, 8),    # 冬季風速中等
        2: (5, 8),    # 冬季風速中等
        3: (5, 8),    # 冬季風速中等
        4: (5, 8),    # 冬季風速中等
        5: (3, 5),    # 春季風速較小
        6: (3, 5)     # 春季風速較小
    }

    print("歡迎使用NCHU風力發電站模擬系統！")
    know_wind_hours = input("請問是否知道今天的風速持續時間？(是/否) ").strip().lower()

    if know_wind_hours == "是":
        turbine_speed_min = float(input("請輸入風速範圍下限（m/s）,勿低於0m/s："))
        while turbine_speed_min < speed_Min:
            turbine_speed_min = float(input(f"風速範圍下限超出範圍，請重新輸入（不超過{ speed_Min } m/s）："))
        turbine_speed_max = float(input("請輸入風速範圍上限（m/s）,勿超過61.2m/s："))

        while turbine_speed_max <= turbine_speed_min or turbine_speed_max > speed_Max:
            if turbine_speed_max <= turbine_speed_min:
                turbine_speed_max = float(input(f"風速範圍上限必須大於下限 {turbine_speed_min} m/s，請重新輸入："))
            else:
                turbine_speed_max = float(input(f"風速範圍上限不能超過 { speed_Max } m/s，請重新輸入："))

        hours_of_wind = int(input("請輸入風速持續時間（小時）："))

    elif know_wind_hours == "否":
         hours_of_wind = 12
         print(f"那在這邊提醒一下使用者，系統目前預設風速持續時間為：{hours_of_wind}小時，謝謝！")
         month = int(input("請輸入現在的月份（1-12）："))
         if month in month_wind_speeds:
           wind_speed_range = month_wind_speeds[month]
         else:
           print("無法識別的月份，將使用預設風速範圍。")
           wind_speed_range = (5, 10)  # 使用預設風速範圍

         print(f"預設風速範圍為：{wind_speed_range[0]} m/s 到 {wind_speed_range[1]} m/s")

         # 隨機選擇下限，排除最大預設風速值
         turbine_speed_min = random.randint(wind_speed_range[0], wind_speed_range[1] - 1)
         print(f"目前的風速範圍下限設定為：{turbine_speed_min} m/s")

         # 隨機選擇上限，要確保上限大於下限
         turbine_speed_max = random.randint(turbine_speed_min, wind_speed_range[1])
    while turbine_speed_max <= turbine_speed_min:  # 如果 max 小於等於 min，重新選擇 max
        turbine_speed_max = random.randint(turbine_speed_min, wind_speed_range[1])
    print(f"目前的風速範圍上限設定為：{turbine_speed_max} m/s")


    efficiency = round((0.5 * max_turbine_power * ((turbine_speed_max + turbine_speed_min) / 2) ** 3 * np.pi * turbine_blade_length ** 2) / 1000, 3)

    print(f"目前有 {default_turbine_count} 台風力發電機，每台效率為 {efficiency} kw。")

    simulation_count = int(input("請輸入要模擬的次數："))
    total_energy_produced_all_simulations = 0
    hourly_energy_production_all_simulations = [[] for _ in range(simulation_count)]

    for i in range(simulation_count):
        print(f"風力發電模擬第{i+1}次開始...")
        wind_plant = WindPowerPlant(default_turbine_count, efficiency)
        wind_plant.generate_energy(hours_of_wind)
        hourly_energy_production = wind_plant.get_hourly_energy_production()
        total_energy_produced_all_simulations += sum(hourly_energy_production)
        hourly_energy_production_all_simulations[i] = hourly_energy_production
        print(f"風力發電模擬第{i+1}次結束。")

    
    print("感謝您參與本次風力發電站的操作！祝您一路順風~")
    return  wind_plant.get_total_energy_produced()
def query_nuclear_energy():# 調用核能發電站程式，返回電量
    
    default_reactor_count = 4
    max_reactor_output = 2000
    operation_hours = 24

    efficiency = round((max_reactor_output * default_reactor_count) / (operation_hours), 3)

    print("歡迎使用NTUST核能發電系統模擬器！")
    print(f"目前有 {default_reactor_count} 個反應爐，每個效率為 {efficiency} kw。")

    simulation_count = int(input("請輸入要模擬的次數："))
    total_energy_produced_all_simulations = 0
    hourly_energy_production_all_simulations = [[] for _ in range(simulation_count)]

    for i in range(simulation_count):
        print(f"核能發電模擬第{i+1}次開始...")
        nuclear_plant = NuclearPowerPlant(default_reactor_count, efficiency)
        nuclear_plant.generate_energy(operation_hours)
        hourly_energy_production = nuclear_plant.get_hourly_energy_production()
        total_energy_produced_all_simulations += sum(hourly_energy_production)
        hourly_energy_production_all_simulations[i] = hourly_energy_production
        print(f"核能發電模擬第{i+1}次結束。")
    print("感謝您參與本次核能發電系統的操作！祝您一路順風~")
    return nuclear_plant.get_total_energy_produced() 
def dispatch_power(): #調度電力
   
    print("以下是兩個主要的功能：")
    print("1. 抽調電力")
    print("2. 電能轉移")

    operation_choice = input("請選擇您所需要的模式：")
    
    if operation_choice == '1':
        print("歡迎使用抽調電力模式。")
        # 獲取用戶需要的電力量
        required_energy = float(input("請輸入需要的電量（kw）："))
        # 從各個發電站抽取電力
        extract_energy_from_stations(required_energy)
        
    elif operation_choice == '2':
        print("歡迎使用電能轉移模式")
        # 進行電力轉移
        transfer_energy_between_stations()
    
    else:
        print("請重新選擇。")
        return
def extract_energy_from_stations(required_energy):
    # 從各個發電站抽取電力
    # 在這里根據隨機的方式從各個發電站抽取電力
    # 注意不能抽取超過該發電站的儲存電量的60%
    # 假設有三個發電站
    solar_energy = query_solar_energy()  # 查詢太陽能發電站的當前電力量
    wind_energy = query_wind_energy()    # 查詢風能發電站的當前電力量
    nuclear_energy = query_nuclear_energy()  # 查詢核能發電站的當前電力量
    
    total_energy_available = solar_energy + wind_energy + nuclear_energy
    print(f"您好，目前三個發電站當前之電量大致為 {total_energy_available} kw.")
    # 如果需要的電力量大於總的可用電力量，則無法滿足要求
    if required_energy > total_energy_available:
        print("抱歉，無法滿足您的要求，總的可用電力量不足。")
        return
    # 更新各個發電站的電力量
    #1.太陽能
    print("您好，歡迎提取太陽能系統")
    available_energy = solar_energy
    total_energy_extracted = 0
    hourly_energy_production = [solar_energy] * 24
    while True:
        extract_energy_choice = input("是否要提取能量？(是/否) ").strip().lower()
        if extract_energy_choice != "是":
            break
        amount_to_extract = float(input("請輸入要提取的電量（kw）："))
        print("正在提取能量，請稍候...")
        max_extraction = solar_energy * 0.6
        if amount_to_extract <= max_extraction and amount_to_extract <= solar_energy:
            solar_energy -= amount_to_extract
            available_energy += amount_to_extract
            total_energy_extracted += amount_to_extract
            print(f"成功提取 {amount_to_extract} kw 能量。")
            extraction_index = len(hourly_energy_production) - 1
            hourly_energy_production[extraction_index] -= amount_to_extract
        elif amount_to_extract > max_extraction:
            print("電量提取失敗：提取的電量超過總發電量的60%。")
        else:
            print("能量提取失敗：提取的能量超過總發電量。")
        print(f"剩餘電量: {solar_energy} kw")
        break
    #2.風能
    print("您好，歡迎提取風能系統")
    available_energy_1 = wind_energy
    total_energy_extracted_1= 0
    hourly_energy_production_1 = [wind_energy] * 24
    while True:
        extract_energy_choice = input("是否要提取能量？(是/否) ").strip().lower()
        if extract_energy_choice != "是":
            break
        amount_to_extract = float(input("請輸入要提取的電量（kw）："))
        print("正在提取能量，請稍候...")
        max_extraction = wind_energy * 0.6
        if amount_to_extract <= max_extraction and amount_to_extract <= wind_energy:
            wind_energy -= amount_to_extract
            available_energy_1 += amount_to_extract
            total_energy_extracted_1 += amount_to_extract
            print(f"成功提取 {amount_to_extract} kw 能量。")
            extraction_index = len(hourly_energy_production_1) - 1
            hourly_energy_production_1[extraction_index] -= amount_to_extract
        elif amount_to_extract > max_extraction:
            print("電量提取失敗：提取的電量超過總發電量的60%。")
        else:
            print("能量提取失敗：提取的能量超過總發電量。")
        print(f"剩餘電量: {wind_energy} kw")
        break
    #核能
    print("您好，歡迎提取核能系統")
    available_energy_2 = nuclear_energy
    total_energy_extracted_2= 0
    hourly_energy_production_2 = [nuclear_energy] * 24
    while True:
        extract_energy_choice = input("是否要提取能量？(是/否) ").strip().lower()
        if extract_energy_choice != "是":
            break
        amount_to_extract = float(input("請輸入要提取的電量（kw）："))
        print("正在提取能量，請稍候...")
        max_extraction = nuclear_energy * 0.6
        if amount_to_extract <= max_extraction and amount_to_extract <= nuclear_energy:
            nuclear_energy -= amount_to_extract
            available_energy_2 += amount_to_extract
            total_energy_extracted_2 += amount_to_extract
            print(f"成功提取 {amount_to_extract} kw 能量。")
            extraction_index = len(hourly_energy_production_2) - 1
            hourly_energy_production_2[extraction_index] -= amount_to_extract
        elif amount_to_extract > max_extraction:
            print("電量提取失敗：提取的電量超過總發電量的60%。")
        else:
            print("能量提取失敗：提取的能量超過總發電量。")
        print(f"剩餘電量: {nuclear_energy} kw")
        break
       
    
    # 顯示抽取電力的結果
    print("成功從各個發電站抽取電力：")
    print(f"太陽能發電站抽取電力：{total_energy_extracted}  kw")
    print(f"風能發電站抽取電力：{total_energy_extracted_1} kw")
    print(f"核能發電站抽取電力：{total_energy_extracted_2} kw")
    tot= total_energy_extracted + total_energy_extracted_1 + total_energy_extracted_2
    # 檢查總提取量是否與預設的 required_energy 一致
    if tot != required_energy:
        print("總提取量與預設值不一致，請重新選擇一個發電站進行提取。")
        return extract_energy_from_stations(required_energy)
def transfer_energy_between_stations():
    # 電力轉移操作
    # 在這里進行發電站之間的電力轉移
    # 注意不能抽取超過該發電站的儲存電量的60%
    # 查詢各個發電站的當前電力量
    solar_energy = query_solar_energy()  # 查詢太陽能發電站的當前電力量
    wind_energy = query_wind_energy()    # 查詢風能發電站的當前電力量
    nuclear_energy = query_nuclear_energy()  # 查詢核能發電站的當前電力量
    # 顯示各個發電站的當前電力量
    print("您好，目前各發電站的電量如下：")
    print(f"太陽能發電站：{solar_energy} kw")
    print(f"風能發電站：{wind_energy} kw")
    print(f"核能發電站：{nuclear_energy} kw")

    # 輸入電力轉移的數量和源發電站、目標發電站
    amount_to_transfer = float(input("請輸入要轉移的電量（kw）："))
    source_station = int(input("請輸入源發電站編號（1: 太陽能, 2: 風能, 3: 核能）："))
    target_station = int(input("請輸入目標發電站編號（1: 太陽能, 2: 風能, 3: 核能）："))
    
    # 檢查輸入的發電站編號是否有效
    if source_station not in [1, 2, 3] or target_station not in [1, 2, 3]:
        print("輸入的發電站編號無效，請重新輸入。")
        return

    # 執行電力轉移
    if source_station == 1:
        # 從太陽能發電站轉移電力
       print("您好，歡迎提取太陽能系統")
       available_energy = solar_energy
       total_energy_extracted = 0
       total_energy_extracted_2=0 
       total_energy_extracted_1=0
       hourly_energy_production = [solar_energy] * 24
       while True:
        extract_energy_choice = input("是否要提取能量？(是/否) ").strip().lower()
        if extract_energy_choice != "是":
            break
        amount_to_extract = float(input("請輸入要提取的電量（kw）："))
        print("正在提取能量，請稍候...")
        max_extraction = solar_energy * 0.6
        if amount_to_extract <= max_extraction and amount_to_extract <= solar_energy:
            solar_energy -= amount_to_extract
            available_energy += amount_to_extract
            total_energy_extracted += amount_to_extract
            print(f"成功提取 {amount_to_extract} kw 能量。")
            extraction_index = len(hourly_energy_production) - 1
            hourly_energy_production[extraction_index] -= amount_to_extract
        elif amount_to_extract > max_extraction:
            print("電量提取失敗：提取的電量超過總發電量的60%。")
        else:
            print("能量提取失敗：提取的能量超過總發電量。")
        print(f"剩餘電量: {solar_energy} kw")
        break
    elif source_station == 2:
        # 從風能發電站轉移電力
       print("您好，歡迎提取風能系統")
       total_energy_extracted=0 
       total_energy_extracted_2=0
       available_energy_1 = wind_energy
       total_energy_extracted_1= 0
       hourly_energy_production_1 = [wind_energy] * 24
       while True:
        extract_energy_choice = input("是否要提取能量？(是/否) ").strip().lower()
        if extract_energy_choice != "是":
            break
        amount_to_extract = float(input("請輸入要提取的電量（kw）："))
        print("正在提取能量，請稍候...")
        max_extraction = wind_energy * 0.6
        if amount_to_extract <= max_extraction and amount_to_extract <= wind_energy:
            wind_energy -= amount_to_extract
            available_energy_1 += amount_to_extract
            total_energy_extracted_1 += amount_to_extract
            print(f"成功提取 {amount_to_extract} kw 能量。")
            extraction_index = len(hourly_energy_production_1) - 1
            hourly_energy_production_1[extraction_index] -= amount_to_extract
        elif amount_to_extract > max_extraction:
            print("電量提取失敗：提取的電量超過總發電量的60%。")
        else:
            print("能量提取失敗：提取的能量超過總發電量。")
        print(f"剩餘電量: {wind_energy} kw")
        break
    else:
        # 從核能發電站轉移電力
       print("您好，歡迎提取核能系統")
       total_energy_extracted_1=0 
       total_energy_extracted=0
       available_energy_2 = nuclear_energy
       total_energy_extracted_2= 0
       hourly_energy_production_2 = [nuclear_energy] * 24
       while True:
        extract_energy_choice = input("是否要提取能量？(是/否) ").strip().lower()
        if extract_energy_choice != "是":
            break
        amount_to_extract = float(input("請輸入要提取的電量（kw）："))
        print("正在提取能量，請稍候...")
        max_extraction = nuclear_energy * 0.6
        if amount_to_extract <= max_extraction and amount_to_extract <= nuclear_energy:
            nuclear_energy -= amount_to_extract
            available_energy_2 += amount_to_extract
            total_energy_extracted_2 += amount_to_extract
            print(f"成功提取 {amount_to_extract} kw 能量。")
            extraction_index = len(hourly_energy_production_2) - 1
            hourly_energy_production_2[extraction_index] -= amount_to_extract
        elif amount_to_extract > max_extraction:
            print("電量提取失敗：提取的電量超過總發電量的60%。")
        else:
            print("能量提取失敗：提取的能量超過總發電量。")
        print(f"剩餘電量: {nuclear_energy} kw")
        break
    tot=total_energy_extracted_2 + total_energy_extracted_1 + total_energy_extracted
    if tot!= amount_to_transfer:
        print("提取量與預設值不一致，請重新設定。")
        return transfer_energy_between_stations()

    # 顯示電力轉移結果
    station_labels = {
    1: "太陽能",
    2: "風能",
    3: "核能"
    }
    source_label = station_labels[source_station]
    target_label = station_labels[target_station]
    if source_station == 1:
       print(f"成功從{source_label}發電站 轉移了 {amount_to_transfer} kw 電力到{target_label}發電站 。")
       print(f"那經由轉移動作，{source_label}發電廠目前剩餘電量為 {solar_energy} kw.")
    elif source_station == 2:
       print(f"成功從{source_label}發電站 轉移了 {amount_to_transfer} kw 電力到{target_label}發電站 。")
       print(f"那經由轉移動作，{source_label}發電廠目前剩餘電量為 {wind_energy} kw.")
    else:
       print(f"成功從{source_label}發電站 轉移了 {amount_to_transfer} kw 電力到{target_label}發電站 。")
       print(f"那經由轉移動作，{source_label}發電廠目前剩餘電量為 {nuclear_energy} kw.")
def inquire_status():
    # 查詢各站內部狀態
    print("請選擇您要查詢的發電站類型：")
    print("1. 太陽能發電廠")
    print("2. 風力發電站")
    print("3. 核能發電廠")
    choice = input("請輸入選項編號：").strip()

    if choice == "1":
        default_solar_panel_count = 20
        max_module_power = 5000
        module_area = 1.6
        solar_irradiance = 1000
        efficiency = round((max_module_power / module_area) / solar_irradiance * 100, 3)
        print("歡迎查看太陽能發電站系統！")
        
        solar_panel_count = default_solar_panel_count# 查詢太陽能發電站的太陽能板數量
        solar_efficiency =  efficiency *default_solar_panel_count # 查詢太陽能發電廠的運作效率
        print("太陽能發電廠設備（太陽能電板）的數量：", solar_panel_count)
        print("每塊太陽能板之運作效率：",efficiency,"kw")
        print("太陽能發電廠基本運作效率：", solar_efficiency,"kw")

    elif choice == "2":
         default_turbine_count = 5
         max_turbine_power = 2000
         turbine_blade_length = 15  # 假設風力發電機的葉片長度為15米
        
         
         wind_speed_range = (5, 10)  # 使用預設風速範圍 
         print(f"預設風速範圍為：{wind_speed_range[0]} m/s 到 {wind_speed_range[1]} m/s")
         # 隨機選擇下限，排除最大預設風速值
         turbine_speed_min = random.randint(wind_speed_range[0], wind_speed_range[1] - 1)
         print(f"目前的風速範圍下限設定為：{turbine_speed_min} m/s")

         # 隨機選擇上限，要確保上限大於下限
         turbine_speed_max = random.randint(turbine_speed_min, wind_speed_range[1])
         while turbine_speed_max <= turbine_speed_min:  # 如果 max 小於等於 min，重新選擇 max
             turbine_speed_max = random.randint(turbine_speed_min, wind_speed_range[1])
         print(f"目前的風速範圍上限設定為：{turbine_speed_max} m/s")
         efficiency = round((0.5 * max_turbine_power * ((turbine_speed_max + turbine_speed_min) / 2) ** 3 * np.pi * turbine_blade_length ** 2) / 1000, 3)     
         wind_turbine_count = default_turbine_count# 查詢風力發電站的風力渦輪機數量
         wind_efficiency = efficiency * default_turbine_count # 查詢風力發電站的運作效率
         print("每台風力發電機的運作效率為:",efficiency,"kw" )
         print("風力發電站風力發電機數量：", wind_turbine_count)
         print("風力發電站運作效率：", wind_efficiency,"kw")
    elif choice == "3":
        default_reactor_count = 4
        max_reactor_output = 2000
        operation_hours = 24
        efficiency = round((max_reactor_output * default_reactor_count) / (operation_hours), 3)
        print("歡迎使用核能發電系統！")
        
        reactor_count = default_reactor_count # 查詢核能發電廠的反應器數量
        reactor_efficiency = efficiency * default_reactor_count # 查詢核能發電廠的運作效率
        print("每個反應爐的運作效率為:",efficiency,"kw" )
        print("核能發電廠反應爐數量：", reactor_count)
        print("核能發電廠運作效率：", reactor_efficiency,"kw")
    else:
        print("輸入無效，請輸入有效的選項編號。")

def main():
    # 主程序邏輯
    welcome_message()
    while True:
        service_choice = select_service()
        if service_choice == 1:
            query_energy()
        elif service_choice == 2:
            dispatch_power()
        elif service_choice == 3:
            inquire_status()
        
        another_service = input("是否需要繼續使用服務？(是/否)").strip().lower()
        if another_service != "是":
            print("那在這邊感謝您的使用，祝您一路順風！")
            break

if __name__ == "__main__":
    main()



