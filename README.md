
{
 "cells": [
  {
   "cell_type": "code",
   "execution_count": 24,
   "metadata": {},
   "outputs": [],
   "source": [
    "import numpy as np\n",
    "import pandas as pd\n",
    "from apyori import apriori"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 27,
   "metadata": {},
   "outputs": [],
   "source": [
    "df = pd.read_csv('C:/Intel/uas/dataset_soal No. 4.csv')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 28,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Usia</th>\n",
       "      <th>Kelahiran_ke-</th>\n",
       "      <th>Waktu_Kelahiran</th>\n",
       "      <th>Tekanan_darah</th>\n",
       "      <th>Kelainan_jantung</th>\n",
       "      <th>Caesarian</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>22</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>2</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>26</td>\n",
       "      <td>2</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>26</td>\n",
       "      <td>2</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>28</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>2</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>22</td>\n",
       "      <td>2</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   Usia  Kelahiran_ke-  Waktu_Kelahiran  Tekanan_darah  Kelainan_jantung  \\\n",
       "0    22              1                0              2                 0   \n",
       "1    26              2                0              1                 0   \n",
       "2    26              2                1              1                 0   \n",
       "3    28              1                0              2                 0   \n",
       "4    22              2                0              1                 0   \n",
       "\n",
       "   Caesarian  \n",
       "0          0  \n",
       "1          1  \n",
       "2          0  \n",
       "3          0  \n",
       "4          1  "
      ]
     },
     "execution_count": 28,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 33,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Usia</th>\n",
       "      <th>Kelahiran_ke-</th>\n",
       "      <th>Waktu_Kelahiran</th>\n",
       "      <th>Tekanan_darah</th>\n",
       "      <th>Kelainan_jantung</th>\n",
       "      <th>Caesarian</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>22</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>2</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>26</td>\n",
       "      <td>2</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>26</td>\n",
       "      <td>2</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>28</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>2</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>22</td>\n",
       "      <td>2</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>...</th>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>75</th>\n",
       "      <td>27</td>\n",
       "      <td>2</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>76</th>\n",
       "      <td>33</td>\n",
       "      <td>4</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>77</th>\n",
       "      <td>29</td>\n",
       "      <td>2</td>\n",
       "      <td>1</td>\n",
       "      <td>2</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>78</th>\n",
       "      <td>25</td>\n",
       "      <td>1</td>\n",
       "      <td>2</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>79</th>\n",
       "      <td>24</td>\n",
       "      <td>2</td>\n",
       "      <td>2</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>80 rows ?? 6 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "    Usia  Kelahiran_ke-  Waktu_Kelahiran  Tekanan_darah  Kelainan_jantung  \\\n",
       "0     22              1                0              2                 0   \n",
       "1     26              2                0              1                 0   \n",
       "2     26              2                1              1                 0   \n",
       "3     28              1                0              2                 0   \n",
       "4     22              2                0              1                 0   \n",
       "..   ...            ...              ...            ...               ...   \n",
       "75    27              2                1              1                 0   \n",
       "76    33              4                0              1                 0   \n",
       "77    29              2                1              2                 0   \n",
       "78    25              1                2              0                 0   \n",
       "79    24              2                2              1                 0   \n",
       "\n",
       "    Caesarian  \n",
       "0           0  \n",
       "1           1  \n",
       "2           0  \n",
       "3           0  \n",
       "4           1  \n",
       "..        ...  \n",
       "75          0  \n",
       "76          1  \n",
       "77          1  \n",
       "78          1  \n",
       "79          0  \n",
       "\n",
       "[80 rows x 6 columns]"
      ]
     },
     "execution_count": 33,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 41,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "for i in range (7):\n",
    "    if(df.loc[i]['Usia'] == 'GF'):\n",
    "        plt.scatter(df.loc[i]['Kelahiran_ke-'], df.loc[i]['Caesarian'], s=10, c='r')\n",
    "    elif(df.loc[i]['Usia'] == 'OR'):\n",
    "        plt.scatter(df.loc[i]['Kelahiran_ke-'], df.loc[i]['Caesarian'], s=20, c='y')\n",
    "    else:\n",
    "        plt.scatter(df.loc[i]['Kelahiran_ke-'], df.loc[i]['Caesarian'], s=25, c='b')\n",
    "        \n",
    "plt.grid()\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.8.5"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 4
}
