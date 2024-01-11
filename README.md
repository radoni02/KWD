<h1 style="font-size: 36px;">Online Video Characteristics and Transcoding Time</h1>


Project carried out for the subject of computer-aided decision-making

The project should include:
- Description of the input data and its exploratory analysis/visualisation
- Normalisation or standardisation of data if necessary
- Theoretical introduction to the tool used and its learning methods
- Analysis of the quality of the resulting tool (classifier, regression, ...) using relevant metrics
- Analysis of how the quality of the proposed tool will change if we change the configuration parameters? Have the model parameters been chosen optimally? (cross validation, grid search)

<h2>Description of the input data and its exploratory analysis/visualisation</h2>
<table>
  <thead>
    <tr>
      <th>Column name</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>duration</td>
      <td>Video duration</td>
    </tr>
    <tr>
      <td>codec</td>
      <td>Type of video coding</td>
    </tr>
    <tr>
      <td>width</td>
      <td>Frame width in pixels</td>
    </tr>
    <tr>
      <td>height</td>
      <td>Frame height in pixels</td>
    </tr>
    <tr>
      <td>bitrate</td>
      <td>Video bit rate</td>
    </tr>
    <tr>
      <td>framerate</td>
      <td>Number of frames per second</td>
    </tr>
    <tr>
      <td>i, p, b</td>
      <td>Number of I, P and B frames in the video</td>
    </tr>
    <tr>
      <td>frames</td>
      <td>Total number of frames in the video</td>
    </tr>
    <tr>
      <td>i_size,p_size,b_size</td>
      <td>Size of P, B and I-frames</td>
    </tr>
     <tr>
      <td>size</td>
      <td>Total video size</td>
    </tr>
     <tr>
      <td>o_bitrate</td>
      <td>Video bit rate after compression</td>
    </tr>
    <tr>
      <td>o_framerate</td>
      <td>Frame rate after compression</td>
    </tr>
    <tr>
      <td>o_width,o_height</td>
      <td>Width and height of frame after compression</td>
    </tr>
    <tr>
      <td>umem</td>
      <td>Memory used by the video compression process</td>
    </tr>
    <tr>
      <td>utime</td>
      <td>The time it takes to process video</td>
    </tr>
  </tbody>
</table>
<h3>Exploratory analysis</h3>
  
![image](https://github.com/radoni02/KWD_project/assets/108626591/383511bb-49cc-4aa1-9fe7-f3b2236125fd)
<h3>Exploratory visualisation</h3>
  
![image](https://github.com/radoni02/KWD_project/assets/108626591/48140938-93a9-4025-a140-762e79a96aa1)

Parameters that may have substantial impact on transcoding time are: video resolution (both input and output), bitrate and amount of different types of frames in a video (i-frames, p-frames, b-frames).
Not included in the above heatmap are input and output codecs as those are not represented as numerical values. They might however have an impact on transcoding time and are worth analysing.

<h2>Normalisation or standardisation of data if necessary</h2>
Since 2 columns in the data contained non-numerical values, we converted them into columns using One-Hot Encoding (the number of new columns is the same as the number of different values in the non-numerical columns) so that the resulting data is suitable for regression (all characteristics have numerical values).
<br></br>

![image](https://github.com/radoni02/KWD_project/assets/108626591/1c2c5885-402f-4523-87bd-29472ce5c996)

<h2>Theoretical introduction to the tool used and its learning methods</h2>
<ul>
        <li>
            <h3>Jupyter Notebook</h3>
            <p>An interactive computing environment for creating and sharing documents with live code, equations, visualizations, and narrative text.</p>
        </li>
        <li>
            <h3>Scikit-Learn (sklearn)</h3>
            <p>A machine learning library in Python.</p>
        </li>
        <ul>
            <li>
                <h5>train_test_split</h5>
                <p>A function for splitting data into training and testing sets, commonly used in machine learning workflows.</p>
            </li>
            <li>
                <h5>fit_transform</h5>
                <p>A method used in transformers to fit the model to the data and transform it simultaneously.</p>
            </li>
            <li>
                <h5>transform</h5>
                <p>A method used to apply transformations to the input data based on the learned parameters from fit_transform.</p>
            </li>
            <li>
                <h5>predict</h5>
                <p>A method used to make predictions on new data based on a trained model.</p>
            </li>
            <li>
                <h5>mean_squared_error</h5>
                <p>A metric for evaluating the performance of a regression model by measuring the average squared difference between predicted and actual values.</p>
            </li>
            <li>
                <h5>cross_val_score</h5>
                <p>A function for performing cross-validated scoring of a machine learning model to assess its generalization performance.</p>
            </li>
        </ul>
         <li>
            <h3>Pandas</h3>
            <p>A fast, powerful, and flexible open-source data manipulation and analysis library for Python. It provides data structures like DataFrame for efficient data handling.</p>
        </li>
        <li>
            <h3>NumPy</h3>
            <p>A fundamental package for scientific computing in Python. It provides support for large, multi-dimensional arrays and matrices, along with mathematical functions.</p>
        </li>
        <li>
            <h3>Matplotlib</h3>
            <p>A comprehensive library for creating static, animated, and interactive visualizations in Python. It is often used for creating plots and charts.</p>
        </li>
        <li>
            <h3>Seaborn</h3>
            <p>A statistical data visualization library based on Matplotlib. It provides a high-level interface for drawing attractive and informative statistical graphics.</p>
        </li>
    </ul>

<h2>Analysis of the quality of the resulting tool (classifier, regression, ...) using relevant metrics</h2>

We first carried out tests using linear regression, of course, standardising the data beforehand

![image](https://github.com/radoni02/KWD_project/assets/108626591/39d55780-38f5-4419-ab73-5f9e76996ad5)

We then checked the operation of the polynomialFeatures 

![image](https://github.com/radoni02/KWD_project/assets/108626591/17e15946-ed92-422f-b307-8686bc46a493)

Unfortunately, in the case of our data, the ratio cannot be greater than 2 because the program is not optimal when calculating it.
Polynomial features has too many requirements with this amount of data/features, and RFE doesn't particularly work because it relies on polynomial features
<br></br>
We then tried using DecisionTreeregressor and RandomForestRegressor which produced the beneficial results shown below

![image](https://github.com/radoni02/KWD_project/assets/108626591/b587a6b3-9743-4f9b-a609-bc2083cc693f)

![image](https://github.com/radoni02/KWD_project/assets/108626591/58bce735-015c-47de-9294-c8f5cecefc35)

<table>
  <tr>
    <th>Model</th>
    <th>MSE</th>
    <th>R2 Score</th>
    <th>Best Hyperparameters</th>
  </tr>
  <tr>
    <td>Linear Regression</td>
    <td>90.3715</td>
    <td>0.6478</td>
    <td>{}</td>
  </tr>
  <tr>
    <td>Decision Tree Regression</td>
    <td>6.4607</td>
    <td>0.9748</td>
    <td>{'max_depth': 30, 'min_samples_split': 2}</td>
  </tr>
  <tr>
    <td>Random Forest Regression</td>
    <td>3.4193</td>
    <td>0.9867</td>
    <td>{'max_depth': 30, 'min_samples_split': 2, 'n_estimators': 200}</td>
  </tr>
</table>


In conclusion, the ensemble approach of the Random Forest, coupled with meticulous hyperparameter tuning, has resulted in superior regression performance compared to both Linear Regression and Decision Tree models. These findings provide valuable insights for selecting the most suitable model for predictive tasks in this context

<h2>Analysis of how the quality of the proposed tool will change if we change the configuration parameters? Have the model parameters been chosen optimally? (cross validation, grid search)</h2>
