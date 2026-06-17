**第一步：打开Anaconda Prompt**

输入安装依赖命令：

pip install pylusat geopandas rasterio shapely

**第二步： 打开代码所在文件夹的目录（代码仓库目录）**

D: （先输入所在盘-替换自己的盘）

cd lcx\\qudong\\pylusat-0.5.0（替换自己的目录）

**第三步：启动jupyter复现代码**

输入命令：jupyter notebook

![](media/image1.png){width="5.758333333333334in"
height="2.577777777777778in"}

**第四步：找到 plots**

依次打开line_density.ipynb

import matplotlib.pyplot as plt\
%matplotlib inline\
from matplotlib import patches\
import numpy as np\
import pandas as pd\
import geopandas as gpd\
import matplotlib\
from rasterio.plot import show\
from matplotlib.patches import Polygon\
from matplotlib.collections import PatchCollection\
streets_gdf =
gpd.read_file(\"./../pylusat/datasets/streets/streets.shp\")\
from pylusat.utils import rasterize_geometry\
streets_arr = rasterize_geometry(streets_gdf, 20)\
ax.set_aspect(\'equal\')\
left, right, bottom, top = 554676, 559500, 622563, 627232\
ax.set_xlim(left, right)\
ax.set_ylim(bottom, top)\
levels = \[0, 1, 2\]\
colors = \[\'white\', \'steelblue\'\]\
cmap, norm = matplotlib.colors.from_levels_and_colors(levels, colors)\
polygon_list = \[\]\
for i in range(3):\
*\# point_list = \[\]\
*for j in range(4):\
*\# x = left + np.random.randint(0, (j+1)\*10)\*100\
\# y = bottom + np.random.randint(0, (j+1)\*10)\*100\
*arr = np.array(to_convex_contour(5, i+j+26))\
arr\[:,0\] = arr\[:,0\]\*1500 + i\*1500 + left + 100\*j\
arr\[:,1\] = arr\[:,1\]\*1500 + i\*1500 + bottom + 100\*j\
polygon = Polygon(arr, edgecolor=\"red\", facecolor=\"red\",\
linewidth=3, alpha=0.4)\
ax.add_patch(polygon)\
show(streets_arr\[0\], cmap=cmap, ax=ax, transform=streets_arr\[1\])\
plt.tight_layout()\
fig.savefig(\"./line_density.png\", dpi=450)

![](media/image2.png){width="3.59375in" height="2.4791666666666665in"}

和 pylusat_performance.ipynb复现

import numpy as np

import pandas as pd

import plotly.graph_objects as go

pnt_dist_csv = \"../pylusat/datasets/csv/pnt_dist.csv\"

pnt_dist_df = pd.read_csv(pnt_dist_csv)

pnt_dist_df\[\'number of points\'\] = pnt_dist_df\[\'number of
points\'\].apply(

lambda x: \"{0:}k\".format(x//1000)

)

fig = go.Figure()

fig.add_trace(go.Bar(

x=pnt_dist_df\[\'number of points\'\],

y=pnt_dist_df\[\'pylusat.dist.to_point()\'\],

name=\'pylusat.dist.to_point()\',

\# marker=dict(

\# color=pnt_dist_df\[\'pylusat dist.to_point()\'\],

\# colorscale=\'Redor\'

\# ),

marker_color=\'rgba(204,204,204,0.5)\',

\# orientation=\'h\'

))

fig.add_trace(go.Bar(

x=pnt_dist_df\[\'number of points\'\],

y=pnt_dist_df\[\'ArcGIS Near Function\'\],

name=\'ArcGIS Near function\',

marker_color=\'rgba(49,130,189,0.7)\',

\# orientation=\'h\'

))

fig.update_traces(texttemplate=\'%{y:.2f}\', textposition=\'outside\')

fig.update_xaxes(showgrid=False, title=\'total number of measurements\')

fig.update_yaxes(showgrid=True, title=\'time cost (s)\',

gridwidth=1, gridcolor=\'gainsboro\')

fig.update_layout(

width=1000, height=470,

showlegend=True,

plot_bgcolor=\'rgba(0,0,0,0)\',

legend=dict(

yanchor=\"bottom\",

y=0.9,

xanchor=\"left\",

x=0,

bgcolor=\'rgba(0,0,0,0)\'

)

)

\# fig.write_image(\"point_dist.png\", scale=5, width=1000, height=470)

fig.show()

line_dist_csv = \"../pylusat/datasets/csv/line_dist.csv\"

line_dist_df = pd.read_csv(line_dist_csv)

line_dist_df\[\'number of points\'\] = line_dist_df\[\'number of
points\'\].apply(

lambda x: \"{0:}k\".format(x//1000)

)

fig = go.Figure()

fig.add_trace(go.Bar(

x=line_dist_df\[\'number of points\'\],

y=line_dist_df\[\'pylusat.dist.to_line()\'\],

name=\'pylusat.dist.to_line()\',

marker_color=\'rgba(204,204,204,0.5)\',

))

fig.add_trace(go.Bar(

x=line_dist_df\[\'number of points\'\],

y=line_dist_df\[\'ArcGIS Near function\'\],

name=\'ArcGIS Near function\',

marker_color=\'rgba(49,130,189,0.7)\',

))

fig.update_traces(texttemplate=\'%{y:.2f}\', textposition=\'outside\')

fig.update_xaxes(showgrid=False, title=\'total number of measurements\')

fig.update_yaxes(showgrid=True, title=\'time cost (s)\',

gridwidth=1, gridcolor=\'gainsboro\')

fig.update_layout(

width=1000, height=470,

showlegend=True,

plot_bgcolor=\'rgba(0,0,0,0)\',

legend=dict(

yanchor=\"top\",

y=0.97,

xanchor=\"left\",

x=0,

bgcolor=\'rgba(0,0,0,0)\'

)

)

\# fig.write_image(\"line_dist.png\", scale=5, width=1000, height=470)

fig.show()

line_den_csv = \"../pylusat/datasets/csv/line_density.csv\"

line_den_df = pd.read_csv(line_den_csv)

line_den_df\[\'total number of measurements\'\] = line_den_df\[\'total
number of measurements\'\].apply(

lambda x: \"{0:}k\".format(x//1000)

)

fig = go.Figure()

fig.add_trace(go.Bar(

x=line_den_df\[\'total number of measurements\'\],

y=line_den_df\[\'pylusat.density.of_line()\'\],

name=\'pylusat.density.of_line()\',

marker_color=\'rgba(204,204,204,0.5)\',

))

fig.add_trace(go.Bar(

x=line_den_df\[\'total number of measurements\'\],

y=line_den_df\[\'ArcGIS model\'\],

name=\'ArcGIS model\',

marker_color=\'rgba(49,130,189,0.7)\',

))

fig.update_traces(texttemplate=\'%{y:.2f}\', textposition=\'outside\')

fig.update_xaxes(showgrid=False, title=\'total number of measurements\')

fig.update_yaxes(showgrid=True, title=\'time cost (s)\',

gridwidth=1, gridcolor=\'gainsboro\')

fig.update_layout(

width=1000, height=470,

showlegend=True,

plot_bgcolor=\'rgba(0,0,0,0)\',

legend=dict(

yanchor=\"top\",

y=0.97,

xanchor=\"left\",

x=0,

bgcolor=\'rgba(0,0,0,0)\'

)

)

\# fig.write_image(\"line_den_eval.png\", scale=5, width=1000,
height=470)

fig.show()

from plotly.subplots import make_subplots

fig = make_subplots(rows=3, cols=1,

shared_xaxes=True,

vertical_spacing=0.02)

fig.add_trace(

go.Bar(

x=pnt_dist_df\[\'number of points\'\],

y=pnt_dist_df\[\'pylusat.dist.to_point()\'\],

name=\'pylusat.dist.to_point()\',

marker_color=\'rgba(204,204,204,0.5)\',

),

row=1, col=1

)

fig.add_trace(

go.Bar(

x=pnt_dist_df\[\'number of points\'\],

y=pnt_dist_df\[\'ArcGIS Near Function\'\],

name=\'ArcGIS Near function\',

marker_color=\'rgba(49,130,189,0.7)\',

),

row=1, col=1

)

fig.add_trace(

go.Bar(

x=line_dist_df\[\'number of points\'\],

y=line_dist_df\[\'pylusat.dist.to_line()\'\],

name=\'pylusat.dist.to_line()\',

marker_color=\'rgba(204,204,204,0.5)\',

),

row=2, col=1

)

fig.add_trace(

go.Bar(

x=line_dist_df\[\'number of points\'\],

y=line_dist_df\[\'ArcGIS Near function\'\],

name=\'ArcGIS Near function\',

marker_color=\'rgba(49,130,189,0.7)\',

),

row=2, col=1

)

fig.add_trace(

go.Bar(

x=line_den_df\[\'total number of measurements\'\],

y=line_den_df\[\'pylusat.density.of_line()\'\],

name=\'pylusat.density.of_line()\',

marker_color=\'rgba(204,204,204,0.5)\',

),

row=3, col=1

)

fig.add_trace(

go.Bar(

x=line_den_df\[\'total number of measurements\'\],

y=line_den_df\[\'ArcGIS model\'\],

name=\'ArcGIS model\',

marker_color=\'rgba(49,130,189,0.7)\',

),

row=3, col=1

)

fig.update_traces(texttemplate=\'%{y:.2f}\', textposition=\'outside\')

fig.update_layout(

width=1000, height=1000,

showlegend=False,

plot_bgcolor=\'rgba(0,0,0,0)\',

)

fig.update_yaxes(showgrid=True, title=\'wall time (s)\',

gridwidth=1, gridcolor=\'gainsboro\')

fig.update_xaxes(showgrid=False, title=\'total number of measurements\',
row=3, col=1)

fig.add_annotation(xref=\"paper\", yref=\"y1\", yanchor=\"top\",

x=0.05, y=129, showarrow=True, arrowhead=7,

arrowsize=3, arrowcolor=\'rgba(204,204,204,0.5)\', standoff=20)

fig.add_annotation(text=\"pylusat.distance.to_point()\", xref=\"paper\",
yref=\"y1\",

x=0.06, y=134, showarrow=False, yanchor=\"bottom\")

fig.add_annotation(xref=\"paper\", yref=\"y1\", yanchor=\"top\",

x=0.05, y=115, showarrow=True, arrowhead=7,

arrowsize=3, arrowcolor=\'rgba(49,130,189,0.7)\', standoff=20)

fig.add_annotation(text=\"ArcGIS \<i\>Near\</i\>\", xref=\"paper\",
yref=\"y1\",

x=0.06, y=120, showarrow=False, yanchor=\"bottom\")

fig.add_annotation(xref=\"paper\", yref=\"y2\", yanchor=\"top\",

x=0.05, y=170, showarrow=True, arrowhead=7,

arrowsize=3, arrowcolor=\'rgba(204,204,204,0.5)\', standoff=20)

fig.add_annotation(text=\"pylusat.distance.to_line()\", xref=\"paper\",
yref=\"y2\",

x=0.06, y=178, showarrow=False, yanchor=\"bottom\")

fig.add_annotation(xref=\"paper\", yref=\"y2\", yanchor=\"top\",

x=0.05, y=150, showarrow=True, arrowhead=7,

arrowsize=3, arrowcolor=\'rgba(49,130,189,0.7)\', standoff=20)

fig.add_annotation(text=\"ArcGIS \<i\>Near\</i\>\", xref=\"paper\",
yref=\"y2\",

x=0.06, y=158, showarrow=False, yanchor=\"bottom\")

fig.add_annotation(xref=\"paper\", yref=\"y3\", yanchor=\"top\",

x=0.05, y=1250, showarrow=True, arrowhead=7,

arrowsize=3, arrowcolor=\'rgba(204,204,204,0.5)\', standoff=20)

fig.add_annotation(text=\"pylusat.density.of_line()\", xref=\"paper\",
yref=\"y3\",

x=0.06, y=1300, showarrow=False, yanchor=\"bottom\")

fig.add_annotation(xref=\"paper\", yref=\"y3\", yanchor=\"top\",

x=0.05, y=1100, showarrow=True, arrowhead=7,

arrowsize=3, arrowcolor=\'rgba(49,130,189,0.7)\', standoff=20)

fig.add_annotation(text=\"an ArcGIS model consisting of \<i\>Line
Density\</i\> and \<i\>Zonal Statistics\</i\>\", xref=\"paper\",
yref=\"y3\",

x=0.06, y=1150, showarrow=False, yanchor=\"bottom\")

fig.write_image(\"eval_performance.png\", scale=5, width=1000,
height=1000)

fig.show()![](media/image3.png){width="5.763194444444444in"
height="4.694444444444445in"}
