# Our First Case Study
For our dataset, we chose to examine data compiled by the World Bank on indicators, such as immunization rates, malnutrition prevalence, and vitamin A supplementation rates across 263 countries around the world. The available data spans 345 indicators collected from 1960-2016.

## Our Persona: Julie
Julie is a former data scientist working for a foundation looking to fund future data science projects on World Health. She wants insights about existing datasets (e.g., the World Bank's Health Indicators) to make decisions about what future data should be collected.


## World Bank Dataset: Integrity
Because it is such a large dataset, we first wanted to examine the integrity of the data by year. We suspected that the dataset would be more complete in more recent years. Figure 1, below, shows the number of useful (non-null) data points for each year. It shows that, indeed, the dataset grew more complete across time.

![alt text](figures/f1.usefuldatapointsbyyear.png)

<details><code>
    health = pd.read_csv('data/data.csv')
    years = health.columns[4:-1]
    health_columns = np.array(health.count(axis=0))[4:-1]
    fig, ax = plt.subplots(figsize=(10, 5))  
    ax.plot(years, health_columns)
    ax.set_title('Useful Data Points by Year')
    ax.set_xlabel('Years')
    ax.set_ylabel('Number of Useful Points')
    ax.set_ylim(bottom=0)
    ax.set_xticks(years[::10])
    plt.tight_layout()
    plt.show()
    fig.savefig('figures/f1.usefuldatapointsbyyear.png')
    </code></details>
    
 Immunization rate is an important metric of global health. Figure 2, below, plots the average immunization rates observed in the time period 1960-2015 per counties selected on equally spaced intervals across the distribution. The left-hand panel includes those countries having missing data, whereas the right-hand panel excludes them. Importantly, the both distributions share a common shape, suggesting that GLOBAL (not per country) rates of immunization are reasonably represented using either approach.
 
![alt test](figures/f2.immunizationspercountry.png)
<details><code>
    # Immunizations Averaged Across Time Per Country, by AS 
    immunization_groupby = health[health['Indicator Name'].str.contains("Immunization")].groupby(by= ['Country Name']) 
    immunization_groupby_mean = immunization_groupby.mean() 
    per_country_rate = immunization_groupby_mean.transpose().mean(numeric_only=True).sort_values(na_position="first") 
    per_country_rate_subset = per_country_rate[::10] 
    per_country_rate_dropnan = per_country_rate.dropna()[::10] 
    fig2, ax2 = plt.subplots(1,2,figsize=(10,10)) 
    fig2.suptitle("Immunizations Averaged Across Time Per Country\n(1960-2015)", fontsize=18) 
    fig2.text(0.5, .04, 'Immunization Rate', ha='center') 
    ax2[0].barh(per_country_rate_subset.index, per_country_rate_subset) 
    ax2[0].set_yticks(per_country_rate_subset.index) 
    ax2[0].set_title('Including\nMissing Data', fontsize=12) 
    ax2[1].set_yticklabels([]) 
    ax2[1].set_yticks([]) 
    ax3 = ax2[1].twinx() 
    ax3.barh(per_country_rate_dropnan.index, per_country_rate_dropnan, align='center') 
    ax2[1].set_title('Excluding\nMissing Data', fontsize=12) 
    ax3.set_yticks(per_country_rate_dropnan.index) 
    ax3.set_yticklabels(per_country_rate_dropnan.index) 
    ax3.invert_xaxis() #plt.tight_layout() 
    plt.show() 
    fig2.savefig('figures/f2.immunizationspercountry.png', bbox_inches = "tight")
</code></details>

## Immunization
Immunization rate is an important metric of global health. Figure 2, below, plots the average immunization rates observed in the time period 1960-2015 per counties selected on equally spaced intervals across the distribution. The left-hand panel includes those countries having missing data, whereas the right-hand panel excludes them. Importantly, the both distributions share a common shape, suggesting that GLOBAL (not per country) rates of immunization are reasonably represented using either approach.

The word has seen much progress since vaccine immunization was a fresh topic back in the late 1970s. The rate shot up quickly to roughly 60% and continue to show a steep increase til 1990s. Since then, overall immunization has slowly shown improvement to reach ~80%. 

The list of immunization analyzed are as follows:
* 'Immunization, BCG (% of one-year-old children)',
* 'Immunization, DPT (% of children ages 12-23 months)',
* 'Immunization, HepB3 (% of one-year-old children)',
* 'Immunization, Hib3 (% of children ages 12-23 months)',
* 'Immunization, measles (% of children ages 12-23 months)',
* 'Immunization, Pol3 (% of one-year-old children)'

![alt text](figures/f3.immunization.png)
![alt text](figures/f4.immunization2.png)
![alt text](figures/f5.immunization3.png)

## Iodized Salt Consumption
My analysis is trying to find some key points regarding the consumption of the Iodized Salt. I selected all the records related to consumption of the Iodized salt worldwide, then trying to do some research upon that, especially from 1993-2013. 
I counted the mean of the the Iodized salt consumption every year, so I could see the trend through in that 20 years. The highest consumption per year also interested me, so I pull out a bar chart to show that data.

![alt text](figures/f5.saltconsumption.png)

![alt text](figures/f6.saltconsumption.png)