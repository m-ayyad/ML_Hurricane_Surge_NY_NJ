# What is this Repository about?
In this repo, we are pleased ot share trained ML models to predict the maximum storm surge height including the effect of wind-generated waves at 57 stations along the New York and New Jersey coastlines. The stations names and their corresponding longitude and latitude are available in file "stations.csv". Any researcher can use this ML models and cite the realted papers shown at the end of this file.

# The training data set
We used the training data set which are available upon request. It is worth mentioning that we found that 85% of the TC storms generate storm surges less than 0.5 m. This causes the trained ML model to under predict all the high impact Tcs. To overcome this imbalance issue, we divided the training data set at every station into two smaller ones based on the minimum distance between the TC eye and the station. The two data sets contain TCs that pass within and outside a radius of 100 Km from the station. You can find more details in our published papers mentioned at the end of this file.

# What is the used ML model?
After performing grid search over different ML algorithms, we found that Adaptive Boost (AdaBoost) algorithm with Support Vector Regressor (SVR) as the base estimator has the best performance. For TCs that pass within a radius of 100Km from the station, the learning rate is set to 0.09, number of weak learners is set to 15, and the regularization and epsilon-insensitive loss parameters of SVR are set to 90 and 0.09, respectively. For TCs that pass outside a radius of 100Km from the station, learning rate is set to 0.05, number of weak learners is set to 50, and the regularization and epsilon-insensitive loss parameters of SVR are set to 65 and 0.03, respectively. The input parameters should be scaled using the maximum values found in folder "Maximum_value_for_scaling". You will find the scaling parameters for every station for every data set. For further information please refer to the cited papers at the end of this file.

# What is the input to the ML trained model?
The input to these ML models are the Tropical Cyclone (TC) characteristics that generally include the distance between the TC and the station, and maximum sustained wind speed. These ML models work only for the specified stations along NY and NJ coastlines in "stations.csv" file. As previously mentioned, for every station you will find two ML models for DS-1 and DS-2 data sets. The ML models use 13 input parameters that should be defined in the a specific order based on the location of the TC with repect to the station.
### For the TCs that are within the 100 Km radius from the station 
1) minimum distance between TC eye and the station in Km.
2) maximum sustained wind speed (6-hours after the time when the TC is closest to the station) in knots.
3) upper latitude distance (6-hours after the time when the TC is closest to the station) in Km.
4) left longitudinal distance (6-hours after the time when the TC is closest to the station) in Km.
5) right longitudinal distance (6-hours after the time when the TC is closest to the station) in Km.
6) maximum sustained wind speed (at the time when the TC is closest to the station) in knots.
7) lower latitude distance (at the time when the TC is closest to the station) in Km.
8) upper latitude distance (at the time when the TC is closest to the station) in Km.
9) left longitudinal distance (at the time when the TC is closest to the station) in Km.
10) right longitudinal distance (at the time when the TC is closest to the station) in Km.
11) maximum sustained wind speed (6-hours before the time when the TC is closest to the station) in knots.
12) lower latitude distance (6-hours before the time when the TC is closest to the station) in Km.
13) right longitudinal distance (6-hours before the time when the TC is closest to the station) in Km.

### For the TCs that are outside the 100 Km radius from the station 
1) minimum distance between TC eye and the station in Km.
2) maximum sustained wind speed (6-hours after the time when the TC is closest to the station) in knots.
3) lower latitude distance (6-hours after the time when the TC is closest to the station) in Km.
4) upper latitude distance (6-hours after the time when the TC is closest to the station) in Km.
5) left longitudinal distance (6-hours after the time when the TC is closest to the station) in Km.
6) right longitudinal distance (6-hours after the time when the TC is closest to the station) in Km.
7) maximum sustained wind speed (at the time when the TC is closest to the station) in knots.
8) lower latitude distance (at the time when the TC is closest to the station) in Km.
9) upper latitude distance (at the time when the TC is closest to the station) in Km.
10) left longitudinal distance (at the time when the TC is closest to the station) in Km.
11) maximum sustained wind speed (6-hours before the time when the TC is closest to the station) in knots.
12) lower latitude distance (6-hours before the time when the TC is closest to the station) in Km.
13) right longitudinal distance (6-hours before the time when the TC is closest to the station) in Km.

The lower, upper latitudes and upper and lower longitudes are defined as:

"If the eye of the TC is on the right side (above) the point of interest, then the left longitudinal (lower latitudinal) distance is zero and the right longitudinal (upper latitudinal) distance is equal to the distance with a negative sign. If the TC’s eye is on the left side (below) the point of interest, then the right longitudinal (upper latitudinal) distance is zero and the left longitudinal (lower latitudinal) distance is equal to the distance with positive sign."

For best understanding of the choice of the input parameters please refer to the cited papers at the end of this file.

# Example to use the trained ML model
A demonstration on how to use the trained ML models is found in the jupyter notebook "example.ipynb".

# If you want to use this repo, please cite the following papers
```
@article{ayyad2023climate,
  title={Climate Change Impact on Hurricane Storm Surge Hazards in New York/New Jersey Coastlines using Machine-Learning},
  author={Ayyad, Mahmoud and Hajj, Muhammad R and Marsooli, Reza},
  journal={Npj Climate and Atmospheric Science},
  volume={},
  number={},
  pages={},
  year={2023},
  publisher={Nature Publishing Group UK London}
}
```

```
@article{ayyad2022machine,
  title={Machine learning-based assessment of storm surge in the New York metropolitan area},
  author={Ayyad, Mahmoud and Hajj, Muhammad R and Marsooli, Reza},
  journal={Scientific Reports},
  volume={12},
  number={1},
  pages={19215},
  year={2022},
  publisher={Nature Publishing Group UK London}
}
```

```
@article{ayyad2022artificial,
  title={Artificial intelligence for hurricane storm surge hazard assessment},
  author={Ayyad, Mahmoud and Hajj, Muhammad R and Marsooli, Reza},
  journal={Ocean Engineering},
  volume={245},
  pages={110435},
  year={2022},
  publisher={Elsevier}
}
```
