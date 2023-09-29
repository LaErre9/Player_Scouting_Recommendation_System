# ⚽🔍 Player Scouting Recommendation System
> AI-Powered Player Scouting: Scout, Recommend, Elevate Your Team's Game - 👀 This is a Beta version

The **Player Scouting Recommendation System** is a tool designed and engineered for football scouts, coaches and analysts. This system uses advanced information retrieval and artificial intelligence techniques to revolutionize player scouting. By entering a specific player, the system quickly identifies the ten most similar players, offering tailored AI-generated reports to recommend the best player for your team based on team characteristics.

To **try** the python application is **available** [CSV_Version of Player Scouting Recommendation System](https://playerscouting.streamlit.app/)! [DEMO]. <br>
*This is the version without Solr, to try the Solr version follow the readme.txt file locally.*

## 📊 Data Source 

The project sources its data from [FBRef](https://fbref.com/en/), a leading football statistics website. With a database comprising over 200,000 players and teams, FBRef provides rich insights crucial for player performance analysis.

## 💻 Technologies Used 

- **LangChain (v0.0.275)**: Interacts with OpenAI's GPT-3.5 for detailed report generation.
- **Scikit Learn**: Calculates player similarities using cosine similarity and employs K-Means for clustering.
- **Pandas (v1.4.3)**: Handles data manipulation, organization, and analysis.
- **Scipy (v1.9.3)**: Computes correlations between player rankings for in-depth performance evaluation.
- **RougeScore (v0.1.2)**: Evaluates report quality against reference texts.
- **BERTScore (v0.3.13)**: Measures semantic similarity for report quality assessment.
- **Streamlit (v1.23.1)**: Provides an intuitive user interface with an autocomplete player search engine.
- **Apache Solr (v8.11.2)**: Efficiently indexes and retrieves player data.

## 🛠️ Methodological Workflow

1. **Data Collection**: Gathered from FBRef, focusing on the top five European leagues in the 2022-2023 season.
2. **Data Preprocessing**: Cleaned and organized for analysis and efficient indexing.
3. **Solr Integration**: Data imported and indexed into Apache Solr for rapid search capabilities.
4. **Similarity Analysis**: Utilizes vector models and clustering algorithms to identify player similarities.
5. **Scouter AI**: Employs GPT-3.5 to generate detailed, customized player reports.
6. **User Interface**: Implemented using Streamlit for a seamless user experience.

<img src="https://github.com/LaErre9/Player_Scouting_Recommendation_System/blob/main/images/ArchGeneral.png" alt="Arch General" width="500" >


## 🔍 Key Features
#### **Efficient Data Retrieval**: 
Leveraging Apache Solr, quickly find and access player data with Query Dynamic Suggestion System.
##### Code script: 
```python
#### Script for Autocomplete
def search_solr(searchterm: str) -> List[any]:
    # Check if a search term is provided
    if searchterm:
        # Query Solr for player names containing the search term
        res = solr.query('FootballStatsCore', {
            'q': 'Player:' + '*' + searchterm + '*',
            'fl': 'Rk,Player',
            'rows': 100000,
        })
        result = res.docs

        # If results are found
        if result != []:
            # Create a DataFrame from the results
            df_p = pd.DataFrame(result)
            # Extract the 'Rk' and 'Player' columns and clean the data
            df_p['Rk'] = df_p['Rk'].apply(lambda x: x[0])
            df_p['Player'] = df_p['Player'].apply(lambda x: x[0])
            # Return the 'Player' column as autocomplete suggestions
            return df_p['Player']
        else:
            # Return an empty list if no results are found
            return []

# Streamlit search box
selected_value = st_searchbox(
    search_solr,
    key="solr_searchbox",
    placeholder="🔍 Search a Football Player"
)
```
##### Result
<img src="https://github.com/LaErre9/Player_Scouting_Recommendation_System/blob/main/images/SearchEngine.gif" alt="Arch General" width="500" >

#### **Player Similarity**:
Discover players with similar playing styles, attributes, and statistics to your selected player. 
<img src="https://github.com/LaErre9/Player_Scouting_Recommendation_System/blob/main/images/Components.gif" alt="Arch General" width="500" >

#### **AI-Generated Reports**
Receive detailed and personalized player reports powered by state-of-the-art natural language generation with a fix-prompt-form.
<img src="https://github.com/LaErre9/Player_Scouting_Recommendation_System/blob/main/images/ScouterAI.gif" alt="Arch General" width="500" >

## 📄 Doc and complete architecture
The complete [Documentation](https://github.com/LaErre9/Player_Scouting_Recommendation_System/blob/main/Elaborato_IRS_Antonio_Romano_M63001315.pdf). In this doc there are all the details of the project. <br><br>
<img src="https://github.com/LaErre9/Player_Scouting_Recommendation_System/blob/main/images/CompleteArch.png" alt="Arch General" width="600" >


## 🚧 Limits 

The Player Scouting Recommendation System has some limitations that are important to consider:

- **Temporal Limitation** ⏰: The system relies on data updated only within the last year, which may limit the accuracy of recommendations, especially in a context where player performances can change rapidly.
- **Limitations of the dataset** 📊: The use of a dataset limited to the year 2022/2023 makes the results less reliable, as it does not take into account the entire football career of a player. This limitation may negatively influence the recommendations, especially for those players who have had varying performances over the years. It is important to note that the results of the Player Similarity component were particularly influenced by the number of matches played during the season. In practice, the more matches a player played, the more accurate the results obtained by the Player Similarity system were.
- **Dependence on Input Data** 🔄: The quality of recommendations depends on the completeness and accuracy of input data, meaning that incomplete or erroneous information can negatively impact decisions.
- **Lack of Context and Human Intuition** 🤖: The AI may not consider intangible factors such as team chemistry or player personalities, which could be relevant for purchase decisions.
- **Technological Limitations** 💻: The accuracy of recommendations is limited by current AI technology and models, which may not fully assess the breadth of a player's skills.
- **Need for Human Verification** 👥: It is essential for teams to conduct thorough human evaluation before making final player acquisition decisions.
- **Report generation and hallucinations** 📄😵: Report generation by a generative AI model can lead to hallucinations or unreliable information. Despite the use of prompt techniques to mitigate this problem, inaccuracies can still occur, calling into question the reliability of generated reports.


## 📚 Acknowledgments 

The Player Scouting Recommendation System has been developed exclusively for demonstrative and educational purposes. This system was created as part of a project for the *Information Retrieval Systems* examination at the **University of Naples, Federico II**. It is essential to note that the recommendation system presented here is designed as a decision support tool and does not intend to replace any Football Scout or coach. It is a conceptual idea. I would like to express our gratitude to the open-source community for the invaluable tools and libraries that made this project possible. Special thanks to **FBRef** for providing comprehensive football data.

👨‍💻 This project was developed by **Antonio Romano** and is available on the [GitHub page](https://github.com/LaErre9?tab=repositories).

