# DDP-GCN Datasets

### 1. Data Source

All dataset are collected from TOPIS (Transport Operation & Information Service, https://topis.seoul.go.kr/). The website is currently operated in Korea only. The traffic data were collected for a month ranging from Apr 1st, 2018 to Apr 30th, 2018. The datasets were collected using GPS of over 70,000 taxis, where the trajectory samples were collected every 5 minutes and the post data processing was applied to calculate the average traffic speed of each link. 
We randomly select two subsets of the dataset by the different range of coordinates, labeled as Urban1 and Urban2. Urban1 dataset containing 480 links ranges from 203000 to 210000 in x-axis (called 'GRS80TM_X' in dataset) and from 442500 to 449500 in y-axis (called 'GRS80TM_Y' in dataset). Urban2 dataset containing 455 links ranges from 187000 to 194000 in x-axis and from 444000 to 451000 in y-axis.
For detailed introduction of dataset, please refer to our manuscript.


### 2. Data Preprocessing
The standard time interval is set to 5 minutes. The linear interpolation method is used to fill missing values. 
To define the adjacency matrices as in our paper, (1) the distance is evaluated based on the Dijkstra algorithm and injected to the Gaussian kernels, and (2) the direction measure and (3) the positional relationship are evaluated based on the start and end segment coordinates. 
For detailed introduction of dataset, please refer to our manuscript.


### 3. Column Description
(1) coordinates.csv

This file contains the spatial information of each link in GRS80 coordinate system. 
- LINK_ID(int, 4705): Link identification.
- VER_SEQ(int, 207): One link includes several segments in order. VER_SEQ indicate the segment ordering.
- GRS80TM_X, GRS80TM_Y(float): X, Y coordinates of each segment of the link in GRS80TM. (Units: meters)

(2) metadata.csv

This file contains the additional information of each link as listed below.
- LINK_ID(int, 4705): Link identification.
- ROAD(int, 471): Road identification. (We convert Korean names into numbers.)
- START(int, 1653): Start region identification. (We convert Korean names into numbers.)
- END(int, 1650): End region identification. (We convert Korean names into numbers.)
- oppID(int, 4491): Opposite-directional link IDs.
- Highway, Bridge(bool): True for the link is included in highway or bridge. 
- lowLimit, highLimit(int): Legal low/high limit speed of each link.
- Length(int): Length of each link (scale: meter).

(3) spd_5min.h5

This file contains the 5-min speed values after linear interpolation. Because this data size is too large, we uploaded it through the Google Drive.
https://drive.google.com/file/d/1SvlZawwvvkX-ofe8UNho4ZdWzKR0_0hG/view?usp=sharing
- block0_items: Link identification(count: 4736).
- block0_values: 5-min speeds(count: 8640). We interpolate zero or nan values. (Units: km/h)
