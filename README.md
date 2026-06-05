# Electric_Vehicle_Population_Data
1.df.sort_values(by='State') - сортировка всего датафрейма по штатам

2.df.groupby('State').agg({'Electric Range': 'mean'}).sort_values('Electric Range', ascending=False).head() - группировка данных по штатамБ вычисление и вывод среднего знаения Electric Range для каждого штата по убыванию

df.groupby('State')[['City', 'Make', 'Model']].value_counts() - группирует по штату, считает, сколько конкретных моделей конкретных марок в конкретных городах находится в каждом штате

df_WA = df.loc[df['State'] == 'WA'], df_WA.sort_values(by='City', ascending=True) - выводим данные по конкретному штату, внутр сортируем по городам

Анализ датафрейма конкретно по штату WA:

crosstab_city_model = pd.crosstab(df_WA['City'], df_WA['Make'])
crosstab_city_model.loc['Total'] = crosstab_city_model.sum()
def total_cars_for_city(row):
    return row.sum()
crosstab_city_model['Total_cars_for_city'] = crosstab_city_model.apply(total_cars_for_city, axis=1) - создаем сводную таблицу по столбцам City и Make, которая показывает, сколько раз встречается конкретная марка авто в каждом городе штата. Считаем общее количество для каждой марки по всем городам (строка Total), количество машин всех марок для каждого города (столбец Total_cars_for_city), и общее количество автомобилей всех марок(пересечение Total и Total_cars_for_city): решение через функцию

crosstab_make_model = pd.crosstab(df_WA['Make'], df_WA['Model'])
crosstab_make_model.loc['Total'] = crosstab_make_model.sum()
crosstab_make_model['Total_auto_for_make'] = crosstab_make_model.sum(axis=1) - создаем сводную таблицу по столбцам Make и Model. Считаем общее количество конкретно для моделей по всем маркам (строка Total), сколько всего автомобилей у каждой марки (во всех её моделях) (столбец Total_auto_for_make), и общее количество всех автомобилей (всех комбинаций марка-модель)(пересечение Total и Total_auto_for_make): решение без функции
