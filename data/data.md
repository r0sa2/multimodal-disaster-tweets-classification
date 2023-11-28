# Data

We used version 2.0 of the [CrisisMMD: Multimodal Crisis Dataset](https://crisisnlp.qcri.org/crisismmd). The dataset consists of several thousands of manually annotated tweets and images collected during seven major natural disasters including earthquakes, hurricanes, wildfires, and floods that
happened in the year 2017 across different parts of the world. The authors who
created the dataset also introduced 3 associated learning tasks. We worked
on Task 1, which is a binary classification task to determine whether a given
tweet or image is useful for humanitarian aid purposes (“Informative”) or not (“Not informative”). The authors consider a tweet/image as “Informative” if it reports/shows one or more of the following: cautions, advice, and warnings, injured, dead, or affected people, rescue, volunteering, or donation request or effort, damaged houses, damaged roads, damaged buildings; flooded houses,
flooded streets; blocked roads, blocked bridges, blocked pathways; any built structure affected by earthquake, fire, heavy rain, strong winds, gust, etc., disaster area maps. Images showing banners, logos, and cartoons are not considered as “Informative”.

## Folder Structure
We [truncated](https://drive.google.com/file/d/1YW0ZV38GzEJ4OkEdt8zs0ISUoFy8v9n5/view?usp=sharing) the original dataset to only include the files relevant to our task, and used the train/dev/test splits provided by the dataset creators. The folder structure is as follows:
- `data`
    - `data_image/`: Image folder
    - `train.tsv`: Train data
    - `dev.tsv`: Dev data
    - `test.tsv`: Test data

## Data Example & Statistics
Each of the aforementioned TSV files contains the following columns separated by a tab: 
| Column  | Description | Example | 
| ------------- | ------------- | ------------- |
| `event_name`  | Disaster event name  | "california_wildfires" |
| `tweet_id`  | Tweet ID  | 917791291823591425 |
| `image_id`  | Combination of `tweet_id` and an index concatenated with an underscore, where the integer indices represent different images associated with a given tweet  | "917791291823591425_0" |
| `tweet_text`  | Tweet text  | "RT @Cal_OES: PLS SHARE: Weâ€™re capturing wildfire response, recovery info here: https://t.co/r89LKpjLPj https://t.co/HiA1oQF2Ax" |
| `image`  | Relative path of an image inside the "data_image" folder for a given tweet  | "data_image/california_wildfires/10_10_2017/917791291823591425_0.jpg" |
| `label`  | Randomly selected label from `label_text` and `label_image`  | "informative" |
| `label_text`  | "informative" if the text is informative and "not_informative" otherwise  | "informative" |
| `label_image`  | "informative" if the image is informative and "not_informative" otherwise  | "informative" |
| `label_text_image`  | "Positive" if `label_text` and `label_image` are the same and "Negative" otherwise  | "Positive" |

For our text-only strong baseline we used `label_text` as the label, and for all other models we used `label` as the label. The no. of samples and % of "informative" labels for each dataset are as follows:

| Dataset  | No. of samples | `label_text` Inf. % | `label` Inf. % |
| ------------- | ------------- | ------------- |  ------------- |
| Train | 13608 | 70.826 | 61.295 |
| Dev | 2237 | 72.061 | 62.897 |
| Test | 2237 | 72.061 | 61.377 |