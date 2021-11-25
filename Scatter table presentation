from numpy import empty
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
# I replace entity column the repetitive word to ''
data = pd.read_excel(r'/Users/misszhang/Desktop/Python practice/excel/covid-testing-all-observations.xlsx')
data['Entity'] = data['Entity'].str.replace(' - tests performed', '')
data['Entity'] = data['Entity'].str.replace(' - people tested', '')
data['Entity'] = data['Entity'].str.replace(' - samples tested', '')
data['Entity'] = data['Entity'].str.replace(' - units unclear', '')
# this comment below is just a record
# data['Entity'] = data['Entity'].map(lambda x: x.rstrip(' - tests performed' and ' - people tested' and ' - sample tested' and ' - units unclear'))

# this is for country input:
country = pd.DataFrame(data, columns = ['Entity'])
country = country.astype(str)
country_name = country.apply(lambda x: x.str.split()).squeeze()
# this is for code input:
code = pd.DataFrame(data, columns = ['ISO code'])
code = code.astype(str)
iso_code = code.apply(lambda x: x.str.split().str[0]).squeeze()

# if you use the test below, you can see albania and costa they all working fine
# but when I run the whole program, it stucks at while loop
"""test1  = data[data['Entity'].str.contains('Albania', case=False)]
print(test1)
test2  = data[data['Entity'].str.contains('Costa Rica', case=False)]
print(test2)"""

# I didn't change the while loop, except small change for names
while True:
    user_input = input('Enter country or ISO code\n')
    # match_result = data['Entity'].str.contains(country_name, case = False).any()
    uppercase = user_input.title()
    match_result = (uppercase == country_name).max()
    print(match_result)
    match_code = (uppercase == iso_code).max()
    if  match_result == True or match_code == True:
        break    
    elif  match_result == False or match_code == False:
        print("Can't find matchable country, reinput!")   
if match_result == True:
    country_info = data[data['Entity'].str.contains(user_input, case=False)]
    user_input = user_input.title()
if match_code == True:
    country_info = data[data['ISO code'].str.contains(user_input, case=False)]
    user_input = user_input.upper()

# this is not changed
graph_type = 'scatter'
graph = pd.DataFrame(country_info, columns = ['Date', 'Cumulative total'])
graph_replace = graph['Cumulative total'].replace('', np.nan)
emptycol = graph_replace.dropna().empty

if emptycol == True:
    print(F"sorry {user_input} no data for Cumulative total")
if emptycol == False:
    graph.plot(x = 'Date', y = 'Cumulative total', kind = graph_type, color = 'blue')
    plt.ylabel = 'Cumulative total'
    plt.title(f'Cumulative increase for {user_input}')
    plt.xticks(rotation=90)
    plt.show()

graph_type2 = 'scatter'
graph2 = pd.DataFrame(country_info, columns = ['Date', 'Daily change in cumulative total'])
graph2_replace = graph2['Daily change in cumulative total'].replace('', np.nan)
emptycol2 = graph2_replace.dropna().empty
if emptycol2 == True:
    print(F"sorry {user_input} no data for Daily change in cumulative total")
elif emptycol2 == False:
    graph2.plot(x = 'Date', y = 'Daily change in cumulative total', kind = graph_type2, color = 'green')
    plt.ylabel = 'Daily change in cumulative total'
    plt.title(f'Daily change for {user_input}')
    plt.xticks(rotation=90)
    plt.show()
