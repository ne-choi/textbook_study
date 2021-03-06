{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "xSaJdgV141dV"
   },
   "source": [
    "# **Pandas 10분 완성(10 Minutes to Pandas) 필사**\n",
    "- 본 자료의 저작권은 [BSD-3-Clause](https://opensource.org/licenses/BSD-3-Clause)이며, [데잇걸즈2가 번역한 Pandas 10분 완성](https://dataitgirls2.github.io/10minutes2pandas/)을 필사한 자료임.\n",
    "\n",
    "**목차**\n",
    "1. Object Creation (객체 생성)  \n",
    "2. Viewing Data (데이터 확인하기)  \n",
    "3. Selection (선택)  \n",
    "4. Missing Data (결측치)  \n",
    "5. Operation (연산)  \n",
    "6. Merge (병합)\n",
    "7. Grouping (그룹화)\n",
    "8. Reshaping (변형)\n",
    "9. Time Series (시계열)\n",
    "10. Categoricals (범주화)\n",
    "11. Plotting (그래프)\n",
    "12. Getting Data In / Out (데이터 입 / 출력)\n",
    "13. Gotchas (잡았다!)\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "id": "bQKAKtir5U7G"
   },
   "outputs": [],
   "source": [
    "# 패키지 불러오기\n",
    "\n",
    "import pandas as pd\n",
    "import numpy as np\n",
    "import matplotlib.pyplot as plt"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "QJSa7bL35noH"
   },
   "source": [
    "## **1. Object Creation**\n",
    "[- 참고: 데이터 구조 소개 섹션](https://pandas.pydata.org/pandas-docs/stable/user_guide/dsintro.html)\n",
    "\n",
    "Pansdas는 값을 가지고 있는 리스트를 통해 [Series](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.html)를 만들고, 정수로 만들어진 인덱스를 기본값으로 불러온다."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/"
    },
    "id": "HVPFOjE458jf",
    "outputId": "47343dda-460e-4519-872a-0f3f62cb1cb9"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0    1.0\n",
       "1    3.0\n",
       "2    5.0\n",
       "3    NaN\n",
       "4    6.0\n",
       "5    8.0\n",
       "dtype: float64"
      ]
     },
     "execution_count": 2,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "s = pd.Series([1, 3, 5, np.nan, 6, 8])\n",
    "s"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "5MZay3pM6EQS"
   },
   "source": [
    "datetime 인덱스와 레이블이 있는 열을 가진 numpy 배열을 전달하여 데이터프레임을 만든다."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/"
    },
    "id": "YYioilEh6KVX",
    "outputId": "00f8ea04-7029-4bc7-f746-ee1159e97732"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "DatetimeIndex(['2013-01-01', '2013-01-02', '2013-01-03', '2013-01-04',\n",
       "               '2013-01-05', '2013-01-06'],\n",
       "              dtype='datetime64[ns]', freq='D')"
      ]
     },
     "execution_count": 3,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "dates = pd.date_range('20130101', periods = 6)\n",
    "dates"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 233
    },
    "id": "6x4Q4TmB6c8I",
    "outputId": "661e50af-dba3-4c82-cf3e-fb567c418541"
   },
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
       "      <th>A</th>\n",
       "      <th>B</th>\n",
       "      <th>C</th>\n",
       "      <th>D</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>2013-01-01</th>\n",
       "      <td>-1.612642</td>\n",
       "      <td>-0.202385</td>\n",
       "      <td>1.369361</td>\n",
       "      <td>0.354048</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-02</th>\n",
       "      <td>-0.414597</td>\n",
       "      <td>0.749837</td>\n",
       "      <td>0.095887</td>\n",
       "      <td>-0.740531</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-03</th>\n",
       "      <td>0.607313</td>\n",
       "      <td>0.782564</td>\n",
       "      <td>0.140000</td>\n",
       "      <td>0.894859</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-04</th>\n",
       "      <td>-0.748149</td>\n",
       "      <td>0.417369</td>\n",
       "      <td>0.823899</td>\n",
       "      <td>1.043707</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-05</th>\n",
       "      <td>-0.420492</td>\n",
       "      <td>-0.175005</td>\n",
       "      <td>-0.021870</td>\n",
       "      <td>-1.980740</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-06</th>\n",
       "      <td>1.494445</td>\n",
       "      <td>-0.582027</td>\n",
       "      <td>1.053088</td>\n",
       "      <td>0.574172</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                   A         B         C         D\n",
       "2013-01-01 -1.612642 -0.202385  1.369361  0.354048\n",
       "2013-01-02 -0.414597  0.749837  0.095887 -0.740531\n",
       "2013-01-03  0.607313  0.782564  0.140000  0.894859\n",
       "2013-01-04 -0.748149  0.417369  0.823899  1.043707\n",
       "2013-01-05 -0.420492 -0.175005 -0.021870 -1.980740\n",
       "2013-01-06  1.494445 -0.582027  1.053088  0.574172"
      ]
     },
     "execution_count": 4,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df = pd.DataFrame(np.random.randn(6, 4), index = dates, columns = list('ABCD'))\n",
    "df"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "Z2Pvjp-36d1z"
   },
   "source": [
    "Series와 같은 것으로 변환될 수 있는 객체들의 dict로 구성된 데이터프레임을 만든다."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 171
    },
    "id": "HrdpgYyP6ibg",
    "outputId": "d8c038e7-c4c3-4886-a346-7c26076e1a0d"
   },
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
       "      <th>A</th>\n",
       "      <th>B</th>\n",
       "      <th>C</th>\n",
       "      <th>D</th>\n",
       "      <th>E</th>\n",
       "      <th>F</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>1.0</td>\n",
       "      <td>2013-01-02</td>\n",
       "      <td>1.0</td>\n",
       "      <td>3</td>\n",
       "      <td>test</td>\n",
       "      <td>foo</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>1.0</td>\n",
       "      <td>2013-01-02</td>\n",
       "      <td>1.0</td>\n",
       "      <td>3</td>\n",
       "      <td>train</td>\n",
       "      <td>foo</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>1.0</td>\n",
       "      <td>2013-01-02</td>\n",
       "      <td>1.0</td>\n",
       "      <td>3</td>\n",
       "      <td>test</td>\n",
       "      <td>foo</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>1.0</td>\n",
       "      <td>2013-01-02</td>\n",
       "      <td>1.0</td>\n",
       "      <td>3</td>\n",
       "      <td>train</td>\n",
       "      <td>foo</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "     A          B    C  D      E    F\n",
       "0  1.0 2013-01-02  1.0  3   test  foo\n",
       "1  1.0 2013-01-02  1.0  3  train  foo\n",
       "2  1.0 2013-01-02  1.0  3   test  foo\n",
       "3  1.0 2013-01-02  1.0  3  train  foo"
      ]
     },
     "execution_count": 5,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df2 = pd.DataFrame({'A': 1.,\n",
    "                    'B': pd.Timestamp('20130102'),\n",
    "                    'C': pd.Series(1, index = list(range(4)), dtype = 'float32'),\n",
    "                    'D': np.array([3] * 4, dtype = 'int32'),\n",
    "                    'E': pd.Categorical([\"test\", \"train\", \"test\", \"train\"]),\n",
    "                    'F': 'foo'})\n",
    "df2"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/"
    },
    "id": "avrhZSha75yU",
    "outputId": "0fd6275d-2b1b-4dc5-ee34-8da4abf15382"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "A           float64\n",
       "B    datetime64[ns]\n",
       "C           float32\n",
       "D             int32\n",
       "E          category\n",
       "F            object\n",
       "dtype: object"
      ]
     },
     "execution_count": 6,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df2.dtypes"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "PbyMCk--7686"
   },
   "source": [
    "## **2. Viewing Data**\n",
    "[- 참고: Basic Section](https://pandas.pydata.org/pandas-docs/stable/user_guide/basics.html)  \n",
    "\n",
    "데이터프레임의 가장 윗줄과 마지막 줄을 확인하고 싶을 때 사용하는 방법 알아보기."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 141
    },
    "id": "JdX7WpmA8VeJ",
    "outputId": "60d98b8f-e537-4fd8-e302-c054cb0bb7e5"
   },
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
       "      <th>A</th>\n",
       "      <th>B</th>\n",
       "      <th>C</th>\n",
       "      <th>D</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>2013-01-04</th>\n",
       "      <td>-0.748149</td>\n",
       "      <td>0.417369</td>\n",
       "      <td>0.823899</td>\n",
       "      <td>1.043707</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-05</th>\n",
       "      <td>-0.420492</td>\n",
       "      <td>-0.175005</td>\n",
       "      <td>-0.021870</td>\n",
       "      <td>-1.980740</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-06</th>\n",
       "      <td>1.494445</td>\n",
       "      <td>-0.582027</td>\n",
       "      <td>1.053088</td>\n",
       "      <td>0.574172</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                   A         B         C         D\n",
       "2013-01-04 -0.748149  0.417369  0.823899  1.043707\n",
       "2013-01-05 -0.420492 -0.175005 -0.021870 -1.980740\n",
       "2013-01-06  1.494445 -0.582027  1.053088  0.574172"
      ]
     },
     "execution_count": 7,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# 괄호() 안에 숫자를 넣으면 (숫자)줄을 불러오고 넣지 않으면 기본값인 5개를 불러옴\n",
    "\n",
    "df.tail(3)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 202
    },
    "id": "nAzYPXXp8ipF",
    "outputId": "9bebab07-bf3d-49f2-baea-2a13bb829aa6"
   },
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
       "      <th>A</th>\n",
       "      <th>B</th>\n",
       "      <th>C</th>\n",
       "      <th>D</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>2013-01-01</th>\n",
       "      <td>-1.612642</td>\n",
       "      <td>-0.202385</td>\n",
       "      <td>1.369361</td>\n",
       "      <td>0.354048</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-02</th>\n",
       "      <td>-0.414597</td>\n",
       "      <td>0.749837</td>\n",
       "      <td>0.095887</td>\n",
       "      <td>-0.740531</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-03</th>\n",
       "      <td>0.607313</td>\n",
       "      <td>0.782564</td>\n",
       "      <td>0.140000</td>\n",
       "      <td>0.894859</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-04</th>\n",
       "      <td>-0.748149</td>\n",
       "      <td>0.417369</td>\n",
       "      <td>0.823899</td>\n",
       "      <td>1.043707</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-05</th>\n",
       "      <td>-0.420492</td>\n",
       "      <td>-0.175005</td>\n",
       "      <td>-0.021870</td>\n",
       "      <td>-1.980740</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                   A         B         C         D\n",
       "2013-01-01 -1.612642 -0.202385  1.369361  0.354048\n",
       "2013-01-02 -0.414597  0.749837  0.095887 -0.740531\n",
       "2013-01-03  0.607313  0.782564  0.140000  0.894859\n",
       "2013-01-04 -0.748149  0.417369  0.823899  1.043707\n",
       "2013-01-05 -0.420492 -0.175005 -0.021870 -1.980740"
      ]
     },
     "execution_count": 8,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.head()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "a6uEU1dP8lZ9"
   },
   "source": [
    "index, column, numpy 데이터 세부 정보를 알아보자."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/"
    },
    "id": "a9_61NCz8sch",
    "outputId": "487f32cd-d4fd-46fc-8689-541a0f142380"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "DatetimeIndex(['2013-01-01', '2013-01-02', '2013-01-03', '2013-01-04',\n",
       "               '2013-01-05', '2013-01-06'],\n",
       "              dtype='datetime64[ns]', freq='D')"
      ]
     },
     "execution_count": 9,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.index"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/"
    },
    "id": "0A2Goupc8tzF",
    "outputId": "767a0f85-a92a-475c-dce1-23964c1ff3d7"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Index(['A', 'B', 'C', 'D'], dtype='object')"
      ]
     },
     "execution_count": 10,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.columns"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/"
    },
    "id": "DZ5JSr7c8urA",
    "outputId": "0c3a5a15-baeb-413e-bacc-064a727537d4"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "array([[-1.61264215, -0.2023848 ,  1.36936106,  0.35404822],\n",
       "       [-0.41459705,  0.74983681,  0.09588737, -0.74053093],\n",
       "       [ 0.60731344,  0.78256437,  0.14000027,  0.89485905],\n",
       "       [-0.74814932,  0.41736876,  0.82389876,  1.04370685],\n",
       "       [-0.42049172, -0.17500487, -0.02187012, -1.98074049],\n",
       "       [ 1.49444451, -0.58202719,  1.0530883 ,  0.57417186]])"
      ]
     },
     "execution_count": 11,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.values"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 294
    },
    "id": "3KXgT79N8x3A",
    "outputId": "be67fd35-2ae7-4553-8af9-2b3922cea0f5"
   },
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
       "      <th>A</th>\n",
       "      <th>B</th>\n",
       "      <th>C</th>\n",
       "      <th>D</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>count</th>\n",
       "      <td>6.000000</td>\n",
       "      <td>6.000000</td>\n",
       "      <td>6.000000</td>\n",
       "      <td>6.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>mean</th>\n",
       "      <td>-0.182354</td>\n",
       "      <td>0.165059</td>\n",
       "      <td>0.576728</td>\n",
       "      <td>0.024252</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>std</th>\n",
       "      <td>1.087357</td>\n",
       "      <td>0.564931</td>\n",
       "      <td>0.582501</td>\n",
       "      <td>1.167331</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>min</th>\n",
       "      <td>-1.612642</td>\n",
       "      <td>-0.582027</td>\n",
       "      <td>-0.021870</td>\n",
       "      <td>-1.980740</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>25%</th>\n",
       "      <td>-0.666235</td>\n",
       "      <td>-0.195540</td>\n",
       "      <td>0.106916</td>\n",
       "      <td>-0.466886</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>50%</th>\n",
       "      <td>-0.417544</td>\n",
       "      <td>0.121182</td>\n",
       "      <td>0.481950</td>\n",
       "      <td>0.464110</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>75%</th>\n",
       "      <td>0.351836</td>\n",
       "      <td>0.666720</td>\n",
       "      <td>0.995791</td>\n",
       "      <td>0.814687</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>max</th>\n",
       "      <td>1.494445</td>\n",
       "      <td>0.782564</td>\n",
       "      <td>1.369361</td>\n",
       "      <td>1.043707</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "              A         B         C         D\n",
       "count  6.000000  6.000000  6.000000  6.000000\n",
       "mean  -0.182354  0.165059  0.576728  0.024252\n",
       "std    1.087357  0.564931  0.582501  1.167331\n",
       "min   -1.612642 -0.582027 -0.021870 -1.980740\n",
       "25%   -0.666235 -0.195540  0.106916 -0.466886\n",
       "50%   -0.417544  0.121182  0.481950  0.464110\n",
       "75%    0.351836  0.666720  0.995791  0.814687\n",
       "max    1.494445  0.782564  1.369361  1.043707"
      ]
     },
     "execution_count": 12,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.describe() # 데이터의 대략적인 통계적 정보 요약을 보여줌"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 171
    },
    "id": "MJTKlY2A82ct",
    "outputId": "f3e4bb6a-bfad-4895-cb15-f36e46f29c69"
   },
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
       "      <th>2013-01-01</th>\n",
       "      <th>2013-01-02</th>\n",
       "      <th>2013-01-03</th>\n",
       "      <th>2013-01-04</th>\n",
       "      <th>2013-01-05</th>\n",
       "      <th>2013-01-06</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>A</th>\n",
       "      <td>-1.612642</td>\n",
       "      <td>-0.414597</td>\n",
       "      <td>0.607313</td>\n",
       "      <td>-0.748149</td>\n",
       "      <td>-0.420492</td>\n",
       "      <td>1.494445</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>B</th>\n",
       "      <td>-0.202385</td>\n",
       "      <td>0.749837</td>\n",
       "      <td>0.782564</td>\n",
       "      <td>0.417369</td>\n",
       "      <td>-0.175005</td>\n",
       "      <td>-0.582027</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>C</th>\n",
       "      <td>1.369361</td>\n",
       "      <td>0.095887</td>\n",
       "      <td>0.140000</td>\n",
       "      <td>0.823899</td>\n",
       "      <td>-0.021870</td>\n",
       "      <td>1.053088</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>D</th>\n",
       "      <td>0.354048</td>\n",
       "      <td>-0.740531</td>\n",
       "      <td>0.894859</td>\n",
       "      <td>1.043707</td>\n",
       "      <td>-1.980740</td>\n",
       "      <td>0.574172</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   2013-01-01  2013-01-02  2013-01-03  2013-01-04  2013-01-05  2013-01-06\n",
       "A   -1.612642   -0.414597    0.607313   -0.748149   -0.420492    1.494445\n",
       "B   -0.202385    0.749837    0.782564    0.417369   -0.175005   -0.582027\n",
       "C    1.369361    0.095887    0.140000    0.823899   -0.021870    1.053088\n",
       "D    0.354048   -0.740531    0.894859    1.043707   -1.980740    0.574172"
      ]
     },
     "execution_count": 13,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.T # 데이터 전치"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 233
    },
    "id": "Tzaypf2n84MH",
    "outputId": "c720d79e-117e-49d1-a58c-95f349540faf"
   },
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
       "      <th>D</th>\n",
       "      <th>C</th>\n",
       "      <th>B</th>\n",
       "      <th>A</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>2013-01-01</th>\n",
       "      <td>0.354048</td>\n",
       "      <td>1.369361</td>\n",
       "      <td>-0.202385</td>\n",
       "      <td>-1.612642</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-02</th>\n",
       "      <td>-0.740531</td>\n",
       "      <td>0.095887</td>\n",
       "      <td>0.749837</td>\n",
       "      <td>-0.414597</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-03</th>\n",
       "      <td>0.894859</td>\n",
       "      <td>0.140000</td>\n",
       "      <td>0.782564</td>\n",
       "      <td>0.607313</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-04</th>\n",
       "      <td>1.043707</td>\n",
       "      <td>0.823899</td>\n",
       "      <td>0.417369</td>\n",
       "      <td>-0.748149</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-05</th>\n",
       "      <td>-1.980740</td>\n",
       "      <td>-0.021870</td>\n",
       "      <td>-0.175005</td>\n",
       "      <td>-0.420492</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-06</th>\n",
       "      <td>0.574172</td>\n",
       "      <td>1.053088</td>\n",
       "      <td>-0.582027</td>\n",
       "      <td>1.494445</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                   D         C         B         A\n",
       "2013-01-01  0.354048  1.369361 -0.202385 -1.612642\n",
       "2013-01-02 -0.740531  0.095887  0.749837 -0.414597\n",
       "2013-01-03  0.894859  0.140000  0.782564  0.607313\n",
       "2013-01-04  1.043707  0.823899  0.417369 -0.748149\n",
       "2013-01-05 -1.980740 -0.021870 -0.175005 -0.420492\n",
       "2013-01-06  0.574172  1.053088 -0.582027  1.494445"
      ]
     },
     "execution_count": 14,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.sort_index(axis = 1, ascending = False) # 축별로 정리"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 233
    },
    "id": "77waGo079ACj",
    "outputId": "1e84f1b8-4b78-4175-9cf9-50237dab5ab3"
   },
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
       "      <th>A</th>\n",
       "      <th>B</th>\n",
       "      <th>C</th>\n",
       "      <th>D</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>2013-01-06</th>\n",
       "      <td>1.494445</td>\n",
       "      <td>-0.582027</td>\n",
       "      <td>1.053088</td>\n",
       "      <td>0.574172</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-01</th>\n",
       "      <td>-1.612642</td>\n",
       "      <td>-0.202385</td>\n",
       "      <td>1.369361</td>\n",
       "      <td>0.354048</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-05</th>\n",
       "      <td>-0.420492</td>\n",
       "      <td>-0.175005</td>\n",
       "      <td>-0.021870</td>\n",
       "      <td>-1.980740</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-04</th>\n",
       "      <td>-0.748149</td>\n",
       "      <td>0.417369</td>\n",
       "      <td>0.823899</td>\n",
       "      <td>1.043707</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-02</th>\n",
       "      <td>-0.414597</td>\n",
       "      <td>0.749837</td>\n",
       "      <td>0.095887</td>\n",
       "      <td>-0.740531</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-03</th>\n",
       "      <td>0.607313</td>\n",
       "      <td>0.782564</td>\n",
       "      <td>0.140000</td>\n",
       "      <td>0.894859</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                   A         B         C         D\n",
       "2013-01-06  1.494445 -0.582027  1.053088  0.574172\n",
       "2013-01-01 -1.612642 -0.202385  1.369361  0.354048\n",
       "2013-01-05 -0.420492 -0.175005 -0.021870 -1.980740\n",
       "2013-01-04 -0.748149  0.417369  0.823899  1.043707\n",
       "2013-01-02 -0.414597  0.749837  0.095887 -0.740531\n",
       "2013-01-03  0.607313  0.782564  0.140000  0.894859"
      ]
     },
     "execution_count": 15,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.sort_values(by = 'B') # 값별로 정렬"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "ya7o63fX9Eh_"
   },
   "source": [
    "## **3. Selection**  \n",
    "* 주석: Pandas에 최적화된 데이터 접근 방법인 .at, .iat, .loc, .iloc 사용  \n",
    "\n",
    "[- 참고: 데이터 인덱싱 및 선택](https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html), [다중 인덱싱/심화 인덱싱](https://pandas.pydata.org/pandas-docs/stable/user_guide/advanced.html)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "OlUtfCYW9hUP"
   },
   "source": [
    "### *** Getting(데이터 얻기)**  \n",
    "df.A와 동일한 Series를 생성하는 단일 열을 선택한다."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/"
    },
    "id": "zrP17CWh9tPV",
    "outputId": "b0568d68-6268-470e-dc08-240a09b1618d"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "2013-01-01   -1.612642\n",
       "2013-01-02   -0.414597\n",
       "2013-01-03    0.607313\n",
       "2013-01-04   -0.748149\n",
       "2013-01-05   -0.420492\n",
       "2013-01-06    1.494445\n",
       "Freq: D, Name: A, dtype: float64"
      ]
     },
     "execution_count": 16,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df['A']"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 141
    },
    "id": "zmhkrleH9vyH",
    "outputId": "191a8ece-211b-45cd-8418-8219dccac813"
   },
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
       "      <th>A</th>\n",
       "      <th>B</th>\n",
       "      <th>C</th>\n",
       "      <th>D</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>2013-01-01</th>\n",
       "      <td>-1.612642</td>\n",
       "      <td>-0.202385</td>\n",
       "      <td>1.369361</td>\n",
       "      <td>0.354048</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-02</th>\n",
       "      <td>-0.414597</td>\n",
       "      <td>0.749837</td>\n",
       "      <td>0.095887</td>\n",
       "      <td>-0.740531</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-03</th>\n",
       "      <td>0.607313</td>\n",
       "      <td>0.782564</td>\n",
       "      <td>0.140000</td>\n",
       "      <td>0.894859</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                   A         B         C         D\n",
       "2013-01-01 -1.612642 -0.202385  1.369361  0.354048\n",
       "2013-01-02 -0.414597  0.749837  0.095887 -0.740531\n",
       "2013-01-03  0.607313  0.782564  0.140000  0.894859"
      ]
     },
     "execution_count": 17,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df[0:3]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 141
    },
    "id": "Vo98mhup9x99",
    "outputId": "070f33df-d968-43e6-943a-02169641a3f7"
   },
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
       "      <th>A</th>\n",
       "      <th>B</th>\n",
       "      <th>C</th>\n",
       "      <th>D</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>2013-01-02</th>\n",
       "      <td>-0.414597</td>\n",
       "      <td>0.749837</td>\n",
       "      <td>0.095887</td>\n",
       "      <td>-0.740531</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-03</th>\n",
       "      <td>0.607313</td>\n",
       "      <td>0.782564</td>\n",
       "      <td>0.140000</td>\n",
       "      <td>0.894859</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-04</th>\n",
       "      <td>-0.748149</td>\n",
       "      <td>0.417369</td>\n",
       "      <td>0.823899</td>\n",
       "      <td>1.043707</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                   A         B         C         D\n",
       "2013-01-02 -0.414597  0.749837  0.095887 -0.740531\n",
       "2013-01-03  0.607313  0.782564  0.140000  0.894859\n",
       "2013-01-04 -0.748149  0.417369  0.823899  1.043707"
      ]
     },
     "execution_count": 18,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df['20130102':'20130104']"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "gL-MwzmE933D"
   },
   "source": [
    "### *** Selection by Label**  \n",
    "[- 참고: Label을 통한 선택](https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/"
    },
    "id": "V2lZZDDc-DJJ",
    "outputId": "fdf5edb2-7312-4341-a5e7-e1ce16256b37"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "A   -1.612642\n",
       "B   -0.202385\n",
       "C    1.369361\n",
       "D    0.354048\n",
       "Name: 2013-01-01 00:00:00, dtype: float64"
      ]
     },
     "execution_count": 19,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# 라벨을 사용하여 횡단면 얻기\n",
    "df.loc[dates[0]]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 233
    },
    "id": "QWsAz6u--N6-",
    "outputId": "d1e1248c-362e-42ba-f9d0-2311b2516a6f"
   },
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
       "      <th>A</th>\n",
       "      <th>B</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>2013-01-01</th>\n",
       "      <td>-1.612642</td>\n",
       "      <td>-0.202385</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-02</th>\n",
       "      <td>-0.414597</td>\n",
       "      <td>0.749837</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-03</th>\n",
       "      <td>0.607313</td>\n",
       "      <td>0.782564</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-04</th>\n",
       "      <td>-0.748149</td>\n",
       "      <td>0.417369</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-05</th>\n",
       "      <td>-0.420492</td>\n",
       "      <td>-0.175005</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-06</th>\n",
       "      <td>1.494445</td>\n",
       "      <td>-0.582027</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                   A         B\n",
       "2013-01-01 -1.612642 -0.202385\n",
       "2013-01-02 -0.414597  0.749837\n",
       "2013-01-03  0.607313  0.782564\n",
       "2013-01-04 -0.748149  0.417369\n",
       "2013-01-05 -0.420492 -0.175005\n",
       "2013-01-06  1.494445 -0.582027"
      ]
     },
     "execution_count": 20,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# 라벨을 사용하여 여러 축(의 데이터) 얻기\n",
    "df.loc[:, ['A', 'B']]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 141
    },
    "id": "a9TUoZtK-W7N",
    "outputId": "54e84cbd-9374-444f-952b-2791a5c9f1af"
   },
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
       "      <th>A</th>\n",
       "      <th>B</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>2013-01-02</th>\n",
       "      <td>-0.414597</td>\n",
       "      <td>0.749837</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-03</th>\n",
       "      <td>0.607313</td>\n",
       "      <td>0.782564</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-04</th>\n",
       "      <td>-0.748149</td>\n",
       "      <td>0.417369</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                   A         B\n",
       "2013-01-02 -0.414597  0.749837\n",
       "2013-01-03  0.607313  0.782564\n",
       "2013-01-04 -0.748149  0.417369"
      ]
     },
     "execution_count": 21,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# 양쪽 종단점을 포함한 라벨 슬라이싱 보기\n",
    "df.loc['20130102':'20130104', ['A', 'B']]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/"
    },
    "id": "z0sKMNSY-hJx",
    "outputId": "fa4a81dd-8a6c-435c-aa60-8a421ba3b118"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "A   -0.414597\n",
       "B    0.749837\n",
       "Name: 2013-01-02 00:00:00, dtype: float64"
      ]
     },
     "execution_count": 22,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# 반환되는 객체의 차원 줄이기\n",
    "df.loc['20130102', ['A', 'B']]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/"
    },
    "id": "EgP3R1zp-l4D",
    "outputId": "75f2cdbc-218a-4b0a-c66d-3f9ddfd113bc"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "-1.6126421545697252"
      ]
     },
     "execution_count": 23,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# 스킬라 값 얻기\n",
    "df.loc[dates[0], 'A']"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/"
    },
    "id": "krORqPkY-p8B",
    "outputId": "aaceb80e-9f3c-446f-f5d6-c8b30932c26c"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "-1.6126421545697252"
      ]
     },
     "execution_count": 24,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# cf. 스킬라 값 더 빠르게 구하는 법\n",
    "df.at[dates[0], 'A']"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "OpnCbJdl-vn4"
   },
   "source": [
    "### *** Selection by Position**  \n",
    "[- 참고: 위치로 선택하기](https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/"
    },
    "id": "xiZeAwfPAA6n",
    "outputId": "6d7c9763-0d7b-4c2e-f3d1-cd68c6760468"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "A   -0.748149\n",
       "B    0.417369\n",
       "C    0.823899\n",
       "D    1.043707\n",
       "Name: 2013-01-04 00:00:00, dtype: float64"
      ]
     },
     "execution_count": 25,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# 넘겨 받은 정수 위치를 기준으로 선택\n",
    "df.iloc[3]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 110
    },
    "id": "dCvmcf93E0rt",
    "outputId": "8509107f-9811-48ac-d4d2-fae8a7956130"
   },
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
       "      <th>A</th>\n",
       "      <th>B</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>2013-01-04</th>\n",
       "      <td>-0.748149</td>\n",
       "      <td>0.417369</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-05</th>\n",
       "      <td>-0.420492</td>\n",
       "      <td>-0.175005</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                   A         B\n",
       "2013-01-04 -0.748149  0.417369\n",
       "2013-01-05 -0.420492 -0.175005"
      ]
     },
     "execution_count": 26,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# 정수로 표기된 슬라이스를 통해, numpy / python과 유사하게 작동\n",
    "df.iloc[3:5, 0:2]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 141
    },
    "id": "g2CyqC3UE7jn",
    "outputId": "48240da6-eaf6-42eb-edad-4f2aa80c8155"
   },
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
       "      <th>A</th>\n",
       "      <th>C</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>2013-01-02</th>\n",
       "      <td>-0.414597</td>\n",
       "      <td>0.095887</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-03</th>\n",
       "      <td>0.607313</td>\n",
       "      <td>0.140000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-05</th>\n",
       "      <td>-0.420492</td>\n",
       "      <td>-0.021870</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                   A         C\n",
       "2013-01-02 -0.414597  0.095887\n",
       "2013-01-03  0.607313  0.140000\n",
       "2013-01-05 -0.420492 -0.021870"
      ]
     },
     "execution_count": 27,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# 정수로 표기된 위치값 리스트를 통해, numpy / python 스타일과 유사해짐\n",
    "df.iloc[[1, 2, 4], [0, 2]]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 110
    },
    "id": "LJEIn2jGFJbl",
    "outputId": "344b3246-666a-4a69-9b29-767c88ed6f3d"
   },
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
       "      <th>A</th>\n",
       "      <th>B</th>\n",
       "      <th>C</th>\n",
       "      <th>D</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>2013-01-02</th>\n",
       "      <td>-0.414597</td>\n",
       "      <td>0.749837</td>\n",
       "      <td>0.095887</td>\n",
       "      <td>-0.740531</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-03</th>\n",
       "      <td>0.607313</td>\n",
       "      <td>0.782564</td>\n",
       "      <td>0.140000</td>\n",
       "      <td>0.894859</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                   A         B         C         D\n",
       "2013-01-02 -0.414597  0.749837  0.095887 -0.740531\n",
       "2013-01-03  0.607313  0.782564  0.140000  0.894859"
      ]
     },
     "execution_count": 28,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# 명시적으로 행을 나누고자 하는 경우\n",
    "df.iloc[1:3, :]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 233
    },
    "id": "3puLloVjJCxB",
    "outputId": "b16564fe-58e6-4d5e-9dd0-4c4debca35f8"
   },
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
       "      <th>B</th>\n",
       "      <th>C</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>2013-01-01</th>\n",
       "      <td>-0.202385</td>\n",
       "      <td>1.369361</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-02</th>\n",
       "      <td>0.749837</td>\n",
       "      <td>0.095887</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-03</th>\n",
       "      <td>0.782564</td>\n",
       "      <td>0.140000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-04</th>\n",
       "      <td>0.417369</td>\n",
       "      <td>0.823899</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-05</th>\n",
       "      <td>-0.175005</td>\n",
       "      <td>-0.021870</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-06</th>\n",
       "      <td>-0.582027</td>\n",
       "      <td>1.053088</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                   B         C\n",
       "2013-01-01 -0.202385  1.369361\n",
       "2013-01-02  0.749837  0.095887\n",
       "2013-01-03  0.782564  0.140000\n",
       "2013-01-04  0.417369  0.823899\n",
       "2013-01-05 -0.175005 -0.021870\n",
       "2013-01-06 -0.582027  1.053088"
      ]
     },
     "execution_count": 29,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# 명시적으로 열을 나누고자 하는 경우\n",
    "df.iloc[:, 1:3]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/"
    },
    "id": "6C8VWQRKJH7P",
    "outputId": "9afb3796-ed5c-4464-e40e-3e4266ba304a"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0.7498368136559216"
      ]
     },
     "execution_count": 30,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# 명시적으로 (특정한) 값을 얻고자 하는 경우\n",
    "df.iloc[1, 1]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/"
    },
    "id": "zPgC89m_Joxi",
    "outputId": "d2fa5eac-1b21-47aa-f426-8355643817b9"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0.7498368136559216"
      ]
     },
     "execution_count": 31,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# 스칼라 값을 빠르게 얻는 방법\n",
    "df.iat[1, 1]"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "DIHDLuXvJ-A8"
   },
   "source": [
    "### *** Boolean Indexing**\n",
    "데이터를 선택하기 위해 단일 열 값을 사용한다.  "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 110
    },
    "id": "fp45t5ZSKHAO",
    "outputId": "8a5ede2d-bb87-40f2-b278-425a5f2e6a74"
   },
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
       "      <th>A</th>\n",
       "      <th>B</th>\n",
       "      <th>C</th>\n",
       "      <th>D</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>2013-01-03</th>\n",
       "      <td>0.607313</td>\n",
       "      <td>0.782564</td>\n",
       "      <td>0.140000</td>\n",
       "      <td>0.894859</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-06</th>\n",
       "      <td>1.494445</td>\n",
       "      <td>-0.582027</td>\n",
       "      <td>1.053088</td>\n",
       "      <td>0.574172</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                   A         B         C         D\n",
       "2013-01-03  0.607313  0.782564  0.140000  0.894859\n",
       "2013-01-06  1.494445 -0.582027  1.053088  0.574172"
      ]
     },
     "execution_count": 32,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df[df.A > 0]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 233
    },
    "id": "yURfYJTbKLTQ",
    "outputId": "bf132053-1a2b-45fe-aaac-54ac71561390"
   },
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
       "      <th>A</th>\n",
       "      <th>B</th>\n",
       "      <th>C</th>\n",
       "      <th>D</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>2013-01-01</th>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>1.369361</td>\n",
       "      <td>0.354048</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-02</th>\n",
       "      <td>NaN</td>\n",
       "      <td>0.749837</td>\n",
       "      <td>0.095887</td>\n",
       "      <td>NaN</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-03</th>\n",
       "      <td>0.607313</td>\n",
       "      <td>0.782564</td>\n",
       "      <td>0.140000</td>\n",
       "      <td>0.894859</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-04</th>\n",
       "      <td>NaN</td>\n",
       "      <td>0.417369</td>\n",
       "      <td>0.823899</td>\n",
       "      <td>1.043707</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-05</th>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-06</th>\n",
       "      <td>1.494445</td>\n",
       "      <td>NaN</td>\n",
       "      <td>1.053088</td>\n",
       "      <td>0.574172</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                   A         B         C         D\n",
       "2013-01-01       NaN       NaN  1.369361  0.354048\n",
       "2013-01-02       NaN  0.749837  0.095887       NaN\n",
       "2013-01-03  0.607313  0.782564  0.140000  0.894859\n",
       "2013-01-04       NaN  0.417369  0.823899  1.043707\n",
       "2013-01-05       NaN       NaN       NaN       NaN\n",
       "2013-01-06  1.494445       NaN  1.053088  0.574172"
      ]
     },
     "execution_count": 33,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# Boolean 조건을 충족하는 데이터프레임에서 값 선택\n",
    "df[df > 0]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 233
    },
    "id": "YWHqyt2SKQbE",
    "outputId": "38a3997a-4725-4644-e8ed-5211b83e69d0"
   },
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
       "      <th>A</th>\n",
       "      <th>B</th>\n",
       "      <th>C</th>\n",
       "      <th>D</th>\n",
       "      <th>E</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>2013-01-01</th>\n",
       "      <td>-1.612642</td>\n",
       "      <td>-0.202385</td>\n",
       "      <td>1.369361</td>\n",
       "      <td>0.354048</td>\n",
       "      <td>one</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-02</th>\n",
       "      <td>-0.414597</td>\n",
       "      <td>0.749837</td>\n",
       "      <td>0.095887</td>\n",
       "      <td>-0.740531</td>\n",
       "      <td>one</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-03</th>\n",
       "      <td>0.607313</td>\n",
       "      <td>0.782564</td>\n",
       "      <td>0.140000</td>\n",
       "      <td>0.894859</td>\n",
       "      <td>two</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-04</th>\n",
       "      <td>-0.748149</td>\n",
       "      <td>0.417369</td>\n",
       "      <td>0.823899</td>\n",
       "      <td>1.043707</td>\n",
       "      <td>three</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-05</th>\n",
       "      <td>-0.420492</td>\n",
       "      <td>-0.175005</td>\n",
       "      <td>-0.021870</td>\n",
       "      <td>-1.980740</td>\n",
       "      <td>four</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-06</th>\n",
       "      <td>1.494445</td>\n",
       "      <td>-0.582027</td>\n",
       "      <td>1.053088</td>\n",
       "      <td>0.574172</td>\n",
       "      <td>three</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                   A         B         C         D      E\n",
       "2013-01-01 -1.612642 -0.202385  1.369361  0.354048    one\n",
       "2013-01-02 -0.414597  0.749837  0.095887 -0.740531    one\n",
       "2013-01-03  0.607313  0.782564  0.140000  0.894859    two\n",
       "2013-01-04 -0.748149  0.417369  0.823899  1.043707  three\n",
       "2013-01-05 -0.420492 -0.175005 -0.021870 -1.980740   four\n",
       "2013-01-06  1.494445 -0.582027  1.053088  0.574172  three"
      ]
     },
     "execution_count": 34,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# 필터링을 위한 메소드 isin()을 사용\n",
    "df2 = df.copy()\n",
    "df2['E'] = ['one', 'one', 'two', 'three', 'four', 'three']\n",
    "df2"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 110
    },
    "id": "UNkCnE7GKen1",
    "outputId": "61932472-822a-4a43-d808-25cf962715b4"
   },
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
       "      <th>A</th>\n",
       "      <th>B</th>\n",
       "      <th>C</th>\n",
       "      <th>D</th>\n",
       "      <th>E</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>2013-01-03</th>\n",
       "      <td>0.607313</td>\n",
       "      <td>0.782564</td>\n",
       "      <td>0.14000</td>\n",
       "      <td>0.894859</td>\n",
       "      <td>two</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-05</th>\n",
       "      <td>-0.420492</td>\n",
       "      <td>-0.175005</td>\n",
       "      <td>-0.02187</td>\n",
       "      <td>-1.980740</td>\n",
       "      <td>four</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                   A         B        C         D     E\n",
       "2013-01-03  0.607313  0.782564  0.14000  0.894859   two\n",
       "2013-01-05 -0.420492 -0.175005 -0.02187 -1.980740  four"
      ]
     },
     "execution_count": 35,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df2[df2['E'].isin(['two', 'four'])]"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "jGK538wGKkwb"
   },
   "source": [
    "### *** Setting**\n",
    "새 열을 설정하면 데이터가 인덱스별로 자동정렬 된다."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/"
    },
    "id": "zrC3kWtUK1L7",
    "outputId": "70017c3a-80fa-485d-e2ca-c9611837a891"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "2013-01-02    1\n",
       "2013-01-03    2\n",
       "2013-01-04    3\n",
       "2013-01-05    4\n",
       "2013-01-06    5\n",
       "2013-01-07    6\n",
       "Freq: D, dtype: int64"
      ]
     },
     "execution_count": 36,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "s1 = pd.Series([1, 2, 3, 4, 5, 6], index = pd.date_range('20130102', periods=6))\n",
    "s1"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "id": "sDKGsL9hK9ze"
   },
   "outputs": [],
   "source": [
    "df['F'] = s1"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "id": "pcL_aOB5LARY"
   },
   "outputs": [],
   "source": [
    "# 라벨에 의해 값 설정\n",
    "df.at[dates[0], 'A'] = 0"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "id": "RZ-lm70JLGVB"
   },
   "outputs": [],
   "source": [
    "# 위치에 의해 값 설정\n",
    "df.iat[0, 1] = 0"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "id": "SNXg2cqpLL1Y"
   },
   "outputs": [],
   "source": [
    "# Numpy 배열을 사용한 할당에 의해 값 설정\n",
    "df.loc[:, 'D'] = np.array([5] * len(df))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 233
    },
    "id": "jtI_KI_dLS9G",
    "outputId": "bf0105b6-65ce-4ce8-ccdd-22ac64632eec"
   },
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
       "      <th>A</th>\n",
       "      <th>B</th>\n",
       "      <th>C</th>\n",
       "      <th>D</th>\n",
       "      <th>F</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>2013-01-01</th>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>1.369361</td>\n",
       "      <td>5</td>\n",
       "      <td>NaN</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-02</th>\n",
       "      <td>-0.414597</td>\n",
       "      <td>0.749837</td>\n",
       "      <td>0.095887</td>\n",
       "      <td>5</td>\n",
       "      <td>1.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-03</th>\n",
       "      <td>0.607313</td>\n",
       "      <td>0.782564</td>\n",
       "      <td>0.140000</td>\n",
       "      <td>5</td>\n",
       "      <td>2.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-04</th>\n",
       "      <td>-0.748149</td>\n",
       "      <td>0.417369</td>\n",
       "      <td>0.823899</td>\n",
       "      <td>5</td>\n",
       "      <td>3.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-05</th>\n",
       "      <td>-0.420492</td>\n",
       "      <td>-0.175005</td>\n",
       "      <td>-0.021870</td>\n",
       "      <td>5</td>\n",
       "      <td>4.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-06</th>\n",
       "      <td>1.494445</td>\n",
       "      <td>-0.582027</td>\n",
       "      <td>1.053088</td>\n",
       "      <td>5</td>\n",
       "      <td>5.0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                   A         B         C  D    F\n",
       "2013-01-01  0.000000  0.000000  1.369361  5  NaN\n",
       "2013-01-02 -0.414597  0.749837  0.095887  5  1.0\n",
       "2013-01-03  0.607313  0.782564  0.140000  5  2.0\n",
       "2013-01-04 -0.748149  0.417369  0.823899  5  3.0\n",
       "2013-01-05 -0.420492 -0.175005 -0.021870  5  4.0\n",
       "2013-01-06  1.494445 -0.582027  1.053088  5  5.0"
      ]
     },
     "execution_count": 41,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# 위 설정대로 작동한 결과\n",
    "df"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 233
    },
    "id": "R40GR1BQLYSr",
    "outputId": "06222e5b-cc6d-4a5b-c706-734327eeb43c"
   },
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
       "      <th>A</th>\n",
       "      <th>B</th>\n",
       "      <th>C</th>\n",
       "      <th>D</th>\n",
       "      <th>F</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>2013-01-01</th>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>-1.369361</td>\n",
       "      <td>-5</td>\n",
       "      <td>NaN</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-02</th>\n",
       "      <td>-0.414597</td>\n",
       "      <td>-0.749837</td>\n",
       "      <td>-0.095887</td>\n",
       "      <td>-5</td>\n",
       "      <td>-1.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-03</th>\n",
       "      <td>-0.607313</td>\n",
       "      <td>-0.782564</td>\n",
       "      <td>-0.140000</td>\n",
       "      <td>-5</td>\n",
       "      <td>-2.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-04</th>\n",
       "      <td>-0.748149</td>\n",
       "      <td>-0.417369</td>\n",
       "      <td>-0.823899</td>\n",
       "      <td>-5</td>\n",
       "      <td>-3.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-05</th>\n",
       "      <td>-0.420492</td>\n",
       "      <td>-0.175005</td>\n",
       "      <td>-0.021870</td>\n",
       "      <td>-5</td>\n",
       "      <td>-4.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-06</th>\n",
       "      <td>-1.494445</td>\n",
       "      <td>-0.582027</td>\n",
       "      <td>-1.053088</td>\n",
       "      <td>-5</td>\n",
       "      <td>-5.0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                   A         B         C  D    F\n",
       "2013-01-01  0.000000  0.000000 -1.369361 -5  NaN\n",
       "2013-01-02 -0.414597 -0.749837 -0.095887 -5 -1.0\n",
       "2013-01-03 -0.607313 -0.782564 -0.140000 -5 -2.0\n",
       "2013-01-04 -0.748149 -0.417369 -0.823899 -5 -3.0\n",
       "2013-01-05 -0.420492 -0.175005 -0.021870 -5 -4.0\n",
       "2013-01-06 -1.494445 -0.582027 -1.053088 -5 -5.0"
      ]
     },
     "execution_count": 42,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# where 연산 설정\n",
    "df2 = df.copy()\n",
    "df2[df2 > 0] = -df2\n",
    "df2"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "Xo2CTZGWLeiD"
   },
   "source": [
    "## **4. Missing Data**\n",
    "Pandas는 결측치를 표현하기 위해, 주로 np.nan 값을 사용한다. (기본 설정값이나 계산에는 포함되지 않음)  \n",
    "[- 참고: Missing data section](https://pandas.pydata.org/pandas-docs/stable/user_guide/missing_data.html)  \n",
    "\n",
    "Reindexing으로 지정된 축 상의 인덱스를 변경/추가/삭제할 수 있다. Reindexing은 데이터의 복사본을 반환한다."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 171
    },
    "id": "WygyjRVKMKJ7",
    "outputId": "378611cd-73f0-4286-d942-e3cf455788ed"
   },
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
       "      <th>A</th>\n",
       "      <th>B</th>\n",
       "      <th>C</th>\n",
       "      <th>D</th>\n",
       "      <th>F</th>\n",
       "      <th>E</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>2013-01-01</th>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>1.369361</td>\n",
       "      <td>5</td>\n",
       "      <td>NaN</td>\n",
       "      <td>1.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-02</th>\n",
       "      <td>-0.414597</td>\n",
       "      <td>0.749837</td>\n",
       "      <td>0.095887</td>\n",
       "      <td>5</td>\n",
       "      <td>1.0</td>\n",
       "      <td>1.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-03</th>\n",
       "      <td>0.607313</td>\n",
       "      <td>0.782564</td>\n",
       "      <td>0.140000</td>\n",
       "      <td>5</td>\n",
       "      <td>2.0</td>\n",
       "      <td>NaN</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-04</th>\n",
       "      <td>-0.748149</td>\n",
       "      <td>0.417369</td>\n",
       "      <td>0.823899</td>\n",
       "      <td>5</td>\n",
       "      <td>3.0</td>\n",
       "      <td>NaN</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                   A         B         C  D    F    E\n",
       "2013-01-01  0.000000  0.000000  1.369361  5  NaN  1.0\n",
       "2013-01-02 -0.414597  0.749837  0.095887  5  1.0  1.0\n",
       "2013-01-03  0.607313  0.782564  0.140000  5  2.0  NaN\n",
       "2013-01-04 -0.748149  0.417369  0.823899  5  3.0  NaN"
      ]
     },
     "execution_count": 43,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df1 = df.reindex(index = dates[0:4], columns = list(df.columns) + ['E'])\n",
    "df1.loc[dates[0]:dates[1], 'E'] = 1\n",
    "df1"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 79
    },
    "id": "YNhLNILbMadU",
    "outputId": "12f29d64-e5a9-4e85-b2e8-ac87b1580d43"
   },
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
       "      <th>A</th>\n",
       "      <th>B</th>\n",
       "      <th>C</th>\n",
       "      <th>D</th>\n",
       "      <th>F</th>\n",
       "      <th>E</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>2013-01-02</th>\n",
       "      <td>-0.414597</td>\n",
       "      <td>0.749837</td>\n",
       "      <td>0.095887</td>\n",
       "      <td>5</td>\n",
       "      <td>1.0</td>\n",
       "      <td>1.0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                   A         B         C  D    F    E\n",
       "2013-01-02 -0.414597  0.749837  0.095887  5  1.0  1.0"
      ]
     },
     "execution_count": 44,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# 결측치를 가지고 있는 행 지우기\n",
    "df1.dropna(how = 'any')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 171
    },
    "id": "NiusFIfkMtvD",
    "outputId": "a6ba6817-c7f0-4537-ca66-f8a96ad4fbc3"
   },
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
       "      <th>A</th>\n",
       "      <th>B</th>\n",
       "      <th>C</th>\n",
       "      <th>D</th>\n",
       "      <th>F</th>\n",
       "      <th>E</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>2013-01-01</th>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>1.369361</td>\n",
       "      <td>5</td>\n",
       "      <td>5.0</td>\n",
       "      <td>1.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-02</th>\n",
       "      <td>-0.414597</td>\n",
       "      <td>0.749837</td>\n",
       "      <td>0.095887</td>\n",
       "      <td>5</td>\n",
       "      <td>1.0</td>\n",
       "      <td>1.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-03</th>\n",
       "      <td>0.607313</td>\n",
       "      <td>0.782564</td>\n",
       "      <td>0.140000</td>\n",
       "      <td>5</td>\n",
       "      <td>2.0</td>\n",
       "      <td>5.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-04</th>\n",
       "      <td>-0.748149</td>\n",
       "      <td>0.417369</td>\n",
       "      <td>0.823899</td>\n",
       "      <td>5</td>\n",
       "      <td>3.0</td>\n",
       "      <td>5.0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                   A         B         C  D    F    E\n",
       "2013-01-01  0.000000  0.000000  1.369361  5  5.0  1.0\n",
       "2013-01-02 -0.414597  0.749837  0.095887  5  1.0  1.0\n",
       "2013-01-03  0.607313  0.782564  0.140000  5  2.0  5.0\n",
       "2013-01-04 -0.748149  0.417369  0.823899  5  3.0  5.0"
      ]
     },
     "execution_count": 45,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# 결측치 채워 넣기\n",
    "df1.fillna(value = 5)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 171
    },
    "id": "ldRf5E9zMy7L",
    "outputId": "c0b07684-a7b6-4887-ff82-4498698cd778"
   },
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
       "      <th>A</th>\n",
       "      <th>B</th>\n",
       "      <th>C</th>\n",
       "      <th>D</th>\n",
       "      <th>F</th>\n",
       "      <th>E</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>2013-01-01</th>\n",
       "      <td>False</td>\n",
       "      <td>False</td>\n",
       "      <td>False</td>\n",
       "      <td>False</td>\n",
       "      <td>True</td>\n",
       "      <td>False</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-02</th>\n",
       "      <td>False</td>\n",
       "      <td>False</td>\n",
       "      <td>False</td>\n",
       "      <td>False</td>\n",
       "      <td>False</td>\n",
       "      <td>False</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-03</th>\n",
       "      <td>False</td>\n",
       "      <td>False</td>\n",
       "      <td>False</td>\n",
       "      <td>False</td>\n",
       "      <td>False</td>\n",
       "      <td>True</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-04</th>\n",
       "      <td>False</td>\n",
       "      <td>False</td>\n",
       "      <td>False</td>\n",
       "      <td>False</td>\n",
       "      <td>False</td>\n",
       "      <td>True</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                A      B      C      D      F      E\n",
       "2013-01-01  False  False  False  False   True  False\n",
       "2013-01-02  False  False  False  False  False  False\n",
       "2013-01-03  False  False  False  False  False   True\n",
       "2013-01-04  False  False  False  False  False   True"
      ]
     },
     "execution_count": 46,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# NAN 값에 boolean을 통한 표식\n",
    "pd.isna(df1) # 데이터프레임의 모든 값이 boolean 형태로 표시되게 하며, nan인 값만 True가 표시되게 하는 함수"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "lCC2VXpLNAqm"
   },
   "source": [
    "## **5. Operation (연산)**\n",
    "[- 참고: 이진(Binary) 연산의 기본 섹션](https://pandas.pydata.org/pandas-docs/stable/user_guide/basics.html)  \n",
    "\n",
    "### *** Stats**\n",
    "통계: 일반적으로 결측치를 제외한 후 연산된다."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/"
    },
    "id": "qLW06Vy3NYvx",
    "outputId": "ec500f38-076e-4696-e83c-0487f5a11d7e"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "A    0.086420\n",
       "B    0.198790\n",
       "C    0.576728\n",
       "D    5.000000\n",
       "F    3.000000\n",
       "dtype: float64"
      ]
     },
     "execution_count": 47,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# 기술통계 수행\n",
    "df.mean()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/"
    },
    "id": "qHL7M8mgNh4J",
    "outputId": "a69a0228-472c-4f49-f2ec-4abb85dc417d"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "2013-01-01    1.592340\n",
       "2013-01-02    1.286225\n",
       "2013-01-03    1.705976\n",
       "2013-01-04    1.698624\n",
       "2013-01-05    1.676527\n",
       "2013-01-06    2.393101\n",
       "Freq: D, dtype: float64"
      ]
     },
     "execution_count": 48,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# 다른 축에서 동일한 연산 수행\n",
    "df.mean(1)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/"
    },
    "id": "DcGzbpD2NmPj",
    "outputId": "16d1a39f-dc83-4e8c-8fa9-099aeaad89d9"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "2013-01-01    NaN\n",
       "2013-01-02    NaN\n",
       "2013-01-03    1.0\n",
       "2013-01-04    3.0\n",
       "2013-01-05    5.0\n",
       "2013-01-06    NaN\n",
       "Freq: D, dtype: float64"
      ]
     },
     "execution_count": 49,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# 정렬이 필요하며, 차원이 다른 객체로 연산 (pandas는 지정된 차원을 따라 자동으로 브로드캐스팅됨)\n",
    "# broadcast: nympy에서 유래, n차원이나 스칼라 값으로 연산 수행 시 도출되는 결과의 규칙을 설명하는 것  \n",
    "s = pd.Series([1, 3, 5, np.nan, 6, 8], index = dates).shift(2)\n",
    "s"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 233
    },
    "id": "4qsZDZIrN8C7",
    "outputId": "322dcf93-760a-4ba1-9005-9944e7d17cd0"
   },
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
       "      <th>A</th>\n",
       "      <th>B</th>\n",
       "      <th>C</th>\n",
       "      <th>D</th>\n",
       "      <th>F</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>2013-01-01</th>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-02</th>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-03</th>\n",
       "      <td>-0.392687</td>\n",
       "      <td>-0.217436</td>\n",
       "      <td>-0.860000</td>\n",
       "      <td>4.0</td>\n",
       "      <td>1.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-04</th>\n",
       "      <td>-3.748149</td>\n",
       "      <td>-2.582631</td>\n",
       "      <td>-2.176101</td>\n",
       "      <td>2.0</td>\n",
       "      <td>0.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-05</th>\n",
       "      <td>-5.420492</td>\n",
       "      <td>-5.175005</td>\n",
       "      <td>-5.021870</td>\n",
       "      <td>0.0</td>\n",
       "      <td>-1.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-06</th>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                   A         B         C    D    F\n",
       "2013-01-01       NaN       NaN       NaN  NaN  NaN\n",
       "2013-01-02       NaN       NaN       NaN  NaN  NaN\n",
       "2013-01-03 -0.392687 -0.217436 -0.860000  4.0  1.0\n",
       "2013-01-04 -3.748149 -2.582631 -2.176101  2.0  0.0\n",
       "2013-01-05 -5.420492 -5.175005 -5.021870  0.0 -1.0\n",
       "2013-01-06       NaN       NaN       NaN  NaN  NaN"
      ]
     },
     "execution_count": 50,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.sub(s, axis = 'index')"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "am44-pxrN_kz"
   },
   "source": [
    "### *** Apply**"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 233
    },
    "id": "uHs-vRp1OM3j",
    "outputId": "a936a233-0c76-4ed6-b513-5f08f4c4cd4b"
   },
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
       "      <th>A</th>\n",
       "      <th>B</th>\n",
       "      <th>C</th>\n",
       "      <th>D</th>\n",
       "      <th>F</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>2013-01-01</th>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>1.369361</td>\n",
       "      <td>5</td>\n",
       "      <td>NaN</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-02</th>\n",
       "      <td>-0.414597</td>\n",
       "      <td>0.749837</td>\n",
       "      <td>1.465248</td>\n",
       "      <td>10</td>\n",
       "      <td>1.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-03</th>\n",
       "      <td>0.192716</td>\n",
       "      <td>1.532401</td>\n",
       "      <td>1.605249</td>\n",
       "      <td>15</td>\n",
       "      <td>3.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-04</th>\n",
       "      <td>-0.555433</td>\n",
       "      <td>1.949770</td>\n",
       "      <td>2.429147</td>\n",
       "      <td>20</td>\n",
       "      <td>6.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-05</th>\n",
       "      <td>-0.975925</td>\n",
       "      <td>1.774765</td>\n",
       "      <td>2.407277</td>\n",
       "      <td>25</td>\n",
       "      <td>10.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2013-01-06</th>\n",
       "      <td>0.518520</td>\n",
       "      <td>1.192738</td>\n",
       "      <td>3.460366</td>\n",
       "      <td>30</td>\n",
       "      <td>15.0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                   A         B         C   D     F\n",
       "2013-01-01  0.000000  0.000000  1.369361   5   NaN\n",
       "2013-01-02 -0.414597  0.749837  1.465248  10   1.0\n",
       "2013-01-03  0.192716  1.532401  1.605249  15   3.0\n",
       "2013-01-04 -0.555433  1.949770  2.429147  20   6.0\n",
       "2013-01-05 -0.975925  1.774765  2.407277  25  10.0\n",
       "2013-01-06  0.518520  1.192738  3.460366  30  15.0"
      ]
     },
     "execution_count": 51,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# 데이터에 함수 적용\n",
    "df.apply(np.cumsum)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/"
    },
    "id": "FoL_xvhdOQf4",
    "outputId": "b6ead426-8aa2-40e4-c821-9754cdb2b932"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "A    2.242594\n",
       "B    1.364592\n",
       "C    1.391231\n",
       "D    0.000000\n",
       "F    4.000000\n",
       "dtype: float64"
      ]
     },
     "execution_count": 52,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.apply(lambda x: x.max() - x.min())"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "akt_tA3kOjs3"
   },
   "source": [
    "### *** Histogramming**\n",
    "[- 참고: Histogramming and Discretization(히스토그래밍과 이산화)](https://pandas.pydata.org/pandas-docs/stable/user_guide/basics.html)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/"
    },
    "id": "iuQZkpuHOvYD",
    "outputId": "800f3aa9-f06b-424e-9a75-fa755e31e164"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0    6\n",
       "1    6\n",
       "2    4\n",
       "3    3\n",
       "4    6\n",
       "5    3\n",
       "6    0\n",
       "7    1\n",
       "8    0\n",
       "9    4\n",
       "dtype: int64"
      ]
     },
     "execution_count": 53,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "s = pd.Series(np.random.randint(0, 7, size = 10))\n",
    "s"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/"
    },
    "id": "Jb2TegwmO0Ya",
    "outputId": "7d1e060b-0af2-43f9-fc85-6565b3bc3313"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<bound method IndexOpsMixin.value_counts of 0    6\n",
       "1    6\n",
       "2    4\n",
       "3    3\n",
       "4    6\n",
       "5    3\n",
       "6    0\n",
       "7    1\n",
       "8    0\n",
       "9    4\n",
       "dtype: int64>"
      ]
     },
     "execution_count": 54,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "s.value_counts"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "R19wY2f8O9PR"
   },
   "source": [
    "### *** String Methods**\n",
    "Series는 문자열 처리 메소드 모음(set)을 가지고 있다.  \n",
    "이 모음은 배열의 각 요소를 쉽게 조작하도록 만드는 문자열의 속성에 포함되어 있다.  \n",
    "문자열의 패턴 일치 확인은 기본적으로 정규 표현식을 사용하며, 몇몇 경우에는 항상 정규 표현식을 사용한다.  \n",
    "\n",
    "[- 참고: 벡터화된 문자열 메소드](https://pandas.pydata.org/pandas-docs/stable/user_guide/text.html)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/"
    },
    "id": "SOKxpfF-PQs8",
    "outputId": "ea724c7b-5caf-45ff-b116-660f43dc0a7a"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0       a\n",
       "1       b\n",
       "2       c\n",
       "3    aaba\n",
       "4    baca\n",
       "5     NaN\n",
       "6    caba\n",
       "7     dog\n",
       "8     cat\n",
       "dtype: object"
      ]
     },
     "execution_count": 55,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "s = pd.Series(['A', 'B', 'C', 'Aaba', 'Baca', np.nan, 'CABA', 'dog', 'cat'])\n",
    "s.str.lower()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "38EfcJTVPe4M"
   },
   "source": [
    "## **6. Merge**  \n",
    "\n",
    "### *** Concat (연결)**\n",
    "결합(join)/병합(merge) 형태의 연산에 관한 인덱스, 관계 대수 기능을 위한 다양한 형태의 논리를 포함한 Series, 데이터프레임, Panel 객체를 손쉽게 결합하는 기능이 있다.  \n",
    "\n",
    "[- 참고: Merging](https://pandas.pydata.org/pandas-docs/stable/user_guide/merging.html)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 355
    },
    "id": "YGe4h4BJP29V",
    "outputId": "b9cb8232-8a72-4281-b4e0-32790677f461"
   },
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
       "      <th>0</th>\n",
       "      <th>1</th>\n",
       "      <th>2</th>\n",
       "      <th>3</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>1.044225</td>\n",
       "      <td>0.155778</td>\n",
       "      <td>0.674068</td>\n",
       "      <td>-1.489455</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>0.504468</td>\n",
       "      <td>-2.412972</td>\n",
       "      <td>-0.541338</td>\n",
       "      <td>0.556083</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>0.849690</td>\n",
       "      <td>0.618393</td>\n",
       "      <td>-0.587040</td>\n",
       "      <td>0.065025</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>-0.112398</td>\n",
       "      <td>0.415087</td>\n",
       "      <td>-0.452262</td>\n",
       "      <td>1.626640</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>1.043760</td>\n",
       "      <td>-1.345565</td>\n",
       "      <td>-0.534134</td>\n",
       "      <td>-0.112001</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5</th>\n",
       "      <td>1.280222</td>\n",
       "      <td>1.533708</td>\n",
       "      <td>0.054365</td>\n",
       "      <td>0.290299</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>6</th>\n",
       "      <td>0.476762</td>\n",
       "      <td>1.399581</td>\n",
       "      <td>0.342671</td>\n",
       "      <td>-0.624159</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>7</th>\n",
       "      <td>0.231877</td>\n",
       "      <td>0.835411</td>\n",
       "      <td>-0.527813</td>\n",
       "      <td>0.502120</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>8</th>\n",
       "      <td>0.268321</td>\n",
       "      <td>-0.991597</td>\n",
       "      <td>0.900198</td>\n",
       "      <td>2.113147</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>9</th>\n",
       "      <td>-0.403591</td>\n",
       "      <td>-0.531963</td>\n",
       "      <td>-1.762530</td>\n",
       "      <td>-2.067926</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "          0         1         2         3\n",
       "0  1.044225  0.155778  0.674068 -1.489455\n",
       "1  0.504468 -2.412972 -0.541338  0.556083\n",
       "2  0.849690  0.618393 -0.587040  0.065025\n",
       "3 -0.112398  0.415087 -0.452262  1.626640\n",
       "4  1.043760 -1.345565 -0.534134 -0.112001\n",
       "5  1.280222  1.533708  0.054365  0.290299\n",
       "6  0.476762  1.399581  0.342671 -0.624159\n",
       "7  0.231877  0.835411 -0.527813  0.502120\n",
       "8  0.268321 -0.991597  0.900198  2.113147\n",
       "9 -0.403591 -0.531963 -1.762530 -2.067926"
      ]
     },
     "execution_count": 56,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# concat()으로 pandas 객체 연결\n",
    "df = pd.DataFrame(np.random.randn(10, 4))\n",
    "df"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 355
    },
    "id": "zh_PiZOnP-OQ",
    "outputId": "66c120ba-0984-4b5d-c76b-8bd89f96fe0f"
   },
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
       "      <th>0</th>\n",
       "      <th>1</th>\n",
       "      <th>2</th>\n",
       "      <th>3</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>1.044225</td>\n",
       "      <td>0.155778</td>\n",
       "      <td>0.674068</td>\n",
       "      <td>-1.489455</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>0.504468</td>\n",
       "      <td>-2.412972</td>\n",
       "      <td>-0.541338</td>\n",
       "      <td>0.556083</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>0.849690</td>\n",
       "      <td>0.618393</td>\n",
       "      <td>-0.587040</td>\n",
       "      <td>0.065025</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>-0.112398</td>\n",
       "      <td>0.415087</td>\n",
       "      <td>-0.452262</td>\n",
       "      <td>1.626640</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>1.043760</td>\n",
       "      <td>-1.345565</td>\n",
       "      <td>-0.534134</td>\n",
       "      <td>-0.112001</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5</th>\n",
       "      <td>1.280222</td>\n",
       "      <td>1.533708</td>\n",
       "      <td>0.054365</td>\n",
       "      <td>0.290299</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>6</th>\n",
       "      <td>0.476762</td>\n",
       "      <td>1.399581</td>\n",
       "      <td>0.342671</td>\n",
       "      <td>-0.624159</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>7</th>\n",
       "      <td>0.231877</td>\n",
       "      <td>0.835411</td>\n",
       "      <td>-0.527813</td>\n",
       "      <td>0.502120</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>8</th>\n",
       "      <td>0.268321</td>\n",
       "      <td>-0.991597</td>\n",
       "      <td>0.900198</td>\n",
       "      <td>2.113147</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>9</th>\n",
       "      <td>-0.403591</td>\n",
       "      <td>-0.531963</td>\n",
       "      <td>-1.762530</td>\n",
       "      <td>-2.067926</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "          0         1         2         3\n",
       "0  1.044225  0.155778  0.674068 -1.489455\n",
       "1  0.504468 -2.412972 -0.541338  0.556083\n",
       "2  0.849690  0.618393 -0.587040  0.065025\n",
       "3 -0.112398  0.415087 -0.452262  1.626640\n",
       "4  1.043760 -1.345565 -0.534134 -0.112001\n",
       "5  1.280222  1.533708  0.054365  0.290299\n",
       "6  0.476762  1.399581  0.342671 -0.624159\n",
       "7  0.231877  0.835411 -0.527813  0.502120\n",
       "8  0.268321 -0.991597  0.900198  2.113147\n",
       "9 -0.403591 -0.531963 -1.762530 -2.067926"
      ]
     },
     "execution_count": 57,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# break it into pieces\n",
    "pieces = [df[:3], df[3:7], df[7:]]\n",
    "pd.concat(pieces)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "gKuNAV8qQJG8"
   },
   "source": [
    "### *** Join**\n",
    "SQL 방식으로 병합한다.  \n",
    "[- 참고: 데이터베이스 스타일 결합](https://pandas.pydata.org/pandas-docs/stable/user_guide/merging.html)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "id": "gcH61KBgQS_K"
   },
   "outputs": [],
   "source": [
    "left = pd.DataFrame({'key': ['foo', 'foo'], 'lval': [1, 2]})\n",
    "right = pd.DataFrame({'key': ['foo', 'foo'], 'rval': [4, 5]})"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 110
    },
    "id": "CXsWDXGpQu2I",
    "outputId": "6cff5e17-3d41-476a-c23c-18e8fc323e55"
   },
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
       "      <th>key</th>\n",
       "      <th>lval</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>foo</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>foo</td>\n",
       "      <td>2</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   key  lval\n",
       "0  foo     1\n",
       "1  foo     2"
      ]
     },
     "execution_count": 59,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "left"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 110
    },
    "id": "5PfcimZaQqV9",
    "outputId": "407cbe62-91e3-43b9-b8b3-56872577930f"
   },
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
       "      <th>key</th>\n",
       "      <th>rval</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>foo</td>\n",
       "      <td>4</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>foo</td>\n",
       "      <td>5</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   key  rval\n",
       "0  foo     4\n",
       "1  foo     5"
      ]
     },
     "execution_count": 60,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "right"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 171
    },
    "id": "PnZp_q0eQqhM",
    "outputId": "694eb9d3-0426-419a-8679-6fce1afc7f3b"
   },
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
       "      <th>key</th>\n",
       "      <th>lval</th>\n",
       "      <th>rval</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>foo</td>\n",
       "      <td>1</td>\n",
       "      <td>4</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>foo</td>\n",
       "      <td>1</td>\n",
       "      <td>5</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>foo</td>\n",
       "      <td>2</td>\n",
       "      <td>4</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>foo</td>\n",
       "      <td>2</td>\n",
       "      <td>5</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   key  lval  rval\n",
       "0  foo     1     4\n",
       "1  foo     1     5\n",
       "2  foo     2     4\n",
       "3  foo     2     5"
      ]
     },
     "execution_count": 61,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "pd.merge(left, right, on = 'key')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "id": "_fHEP5lSQ4SN"
   },
   "outputs": [],
   "source": [
    "# 다른 예시\n",
    "left = pd.DataFrame({'key': ['foo', 'bar'], 'lval': [1, 2]})\n",
    "right = pd.DataFrame({'key': ['foo', 'bar'], 'rval': [4, 5]})"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 110
    },
    "id": "8DSVr11eRKX2",
    "outputId": "ec9534ac-fbe5-462d-bc5c-4f0e9adec780"
   },
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
       "      <th>key</th>\n",
       "      <th>lval</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>foo</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>bar</td>\n",
       "      <td>2</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   key  lval\n",
       "0  foo     1\n",
       "1  bar     2"
      ]
     },
     "execution_count": 63,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "left"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 110
    },
    "id": "SbsqBjk4RMp8",
    "outputId": "7fb4800f-2817-40bb-9cce-cddad341e733"
   },
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
       "      <th>key</th>\n",
       "      <th>rval</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>foo</td>\n",
       "      <td>4</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>bar</td>\n",
       "      <td>5</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   key  rval\n",
       "0  foo     4\n",
       "1  bar     5"
      ]
     },
     "execution_count": 64,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "right"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 110
    },
    "id": "Z-4Vs166ROVh",
    "outputId": "8b177870-03ff-400f-c0e0-1fa1bccc7b6e"
   },
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
       "      <th>key</th>\n",
       "      <th>lval</th>\n",
       "      <th>rval</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>foo</td>\n",
       "      <td>1</td>\n",
       "      <td>4</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>bar</td>\n",
       "      <td>2</td>\n",
       "      <td>5</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   key  lval  rval\n",
       "0  foo     1     4\n",
       "1  bar     2     5"
      ]
     },
     "execution_count": 65,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "pd.merge(left, right, on = 'key')"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "Qa4wVI7oRo9k"
   },
   "source": [
    "### *** Append (추가)**\n",
    "데이터프레임에 행을 추가한다.  \n",
    "[- 참고: Appending](https://pandas.pydata.org/pandas-docs/stable/user_guide/merging.html)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 294
    },
    "id": "NK954e9CRxwr",
    "outputId": "697363fd-a6ca-460c-d0fd-d8e7e478e179"
   },
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
       "      <th>A</th>\n",
       "      <th>B</th>\n",
       "      <th>C</th>\n",
       "      <th>D</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>-1.293826</td>\n",
       "      <td>0.735671</td>\n",
       "      <td>1.108050</td>\n",
       "      <td>-0.175206</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>-1.949366</td>\n",
       "      <td>1.468593</td>\n",
       "      <td>1.386484</td>\n",
       "      <td>0.963284</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>-0.423707</td>\n",
       "      <td>0.157079</td>\n",
       "      <td>0.185440</td>\n",
       "      <td>0.435985</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>-0.478659</td>\n",
       "      <td>1.293856</td>\n",
       "      <td>-0.515603</td>\n",
       "      <td>0.200678</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>0.096275</td>\n",
       "      <td>1.907146</td>\n",
       "      <td>-0.771668</td>\n",
       "      <td>-0.622949</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5</th>\n",
       "      <td>0.557493</td>\n",
       "      <td>0.096811</td>\n",
       "      <td>-0.901813</td>\n",
       "      <td>-0.458602</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>6</th>\n",
       "      <td>-0.072528</td>\n",
       "      <td>-2.372909</td>\n",
       "      <td>-1.428934</td>\n",
       "      <td>1.458320</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>7</th>\n",
       "      <td>-0.199425</td>\n",
       "      <td>-0.455105</td>\n",
       "      <td>0.771140</td>\n",
       "      <td>0.506667</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "          A         B         C         D\n",
       "0 -1.293826  0.735671  1.108050 -0.175206\n",
       "1 -1.949366  1.468593  1.386484  0.963284\n",
       "2 -0.423707  0.157079  0.185440  0.435985\n",
       "3 -0.478659  1.293856 -0.515603  0.200678\n",
       "4  0.096275  1.907146 -0.771668 -0.622949\n",
       "5  0.557493  0.096811 -0.901813 -0.458602\n",
       "6 -0.072528 -2.372909 -1.428934  1.458320\n",
       "7 -0.199425 -0.455105  0.771140  0.506667"
      ]
     },
     "execution_count": 66,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df = pd.DataFrame(np.random.randn(8, 4), columns = ['A', 'B', 'C', 'D'])\n",
    "df"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 325
    },
    "id": "QlXKGdExR67A",
    "outputId": "602a8c78-04d7-4341-ec62-1217cc04d3a6"
   },
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
       "      <th>A</th>\n",
       "      <th>B</th>\n",
       "      <th>C</th>\n",
       "      <th>D</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>-1.293826</td>\n",
       "      <td>0.735671</td>\n",
       "      <td>1.108050</td>\n",
       "      <td>-0.175206</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>-1.949366</td>\n",
       "      <td>1.468593</td>\n",
       "      <td>1.386484</td>\n",
       "      <td>0.963284</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>-0.423707</td>\n",
       "      <td>0.157079</td>\n",
       "      <td>0.185440</td>\n",
       "      <td>0.435985</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>-0.478659</td>\n",
       "      <td>1.293856</td>\n",
       "      <td>-0.515603</td>\n",
       "      <td>0.200678</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>0.096275</td>\n",
       "      <td>1.907146</td>\n",
       "      <td>-0.771668</td>\n",
       "      <td>-0.622949</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5</th>\n",
       "      <td>0.557493</td>\n",
       "      <td>0.096811</td>\n",
       "      <td>-0.901813</td>\n",
       "      <td>-0.458602</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>6</th>\n",
       "      <td>-0.072528</td>\n",
       "      <td>-2.372909</td>\n",
       "      <td>-1.428934</td>\n",
       "      <td>1.458320</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>7</th>\n",
       "      <td>-0.199425</td>\n",
       "      <td>-0.455105</td>\n",
       "      <td>0.771140</td>\n",
       "      <td>0.506667</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>8</th>\n",
       "      <td>-0.478659</td>\n",
       "      <td>1.293856</td>\n",
       "      <td>-0.515603</td>\n",
       "      <td>0.200678</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "          A         B         C         D\n",
       "0 -1.293826  0.735671  1.108050 -0.175206\n",
       "1 -1.949366  1.468593  1.386484  0.963284\n",
       "2 -0.423707  0.157079  0.185440  0.435985\n",
       "3 -0.478659  1.293856 -0.515603  0.200678\n",
       "4  0.096275  1.907146 -0.771668 -0.622949\n",
       "5  0.557493  0.096811 -0.901813 -0.458602\n",
       "6 -0.072528 -2.372909 -1.428934  1.458320\n",
       "7 -0.199425 -0.455105  0.771140  0.506667\n",
       "8 -0.478659  1.293856 -0.515603  0.200678"
      ]
     },
     "execution_count": 67,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "s = df.iloc[3]\n",
    "df.append(s, ignore_index=True)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "GxhzqBGcSHyF"
   },
   "source": [
    "## **7. Grouping**\n",
    "그룹화는 다음 단계 중 하나 이상을 포함하는 과정을 말한다.  \n",
    "- 몇몇 기준에 따라 여러 그룹으로 데이터를 분할(splitting)  \n",
    "- 각 그룹에 독립적으로 함수를 적용(applying)  \n",
    "- 결과물을 하나의 데이터 구조로 결합(combining)  \n",
    "\n",
    "[- 참고: 그룹화](https://pandas.pydata.org/pandas-docs/stable/user_guide/groupby.html)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 294
    },
    "id": "93A1AVKNSZ3f",
    "outputId": "397d0661-edef-4067-e0ff-9ab49532fa82"
   },
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
       "      <th>A</th>\n",
       "      <th>B</th>\n",
       "      <th>C</th>\n",
       "      <th>D</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>foo</td>\n",
       "      <td>one</td>\n",
       "      <td>0.024720</td>\n",
       "      <td>-1.293299</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>bar</td>\n",
       "      <td>one</td>\n",
       "      <td>1.510969</td>\n",
       "      <td>0.509977</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>foo</td>\n",
       "      <td>two</td>\n",
       "      <td>0.342461</td>\n",
       "      <td>-0.811380</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>bar</td>\n",
       "      <td>three</td>\n",
       "      <td>0.227221</td>\n",
       "      <td>0.717127</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>foo</td>\n",
       "      <td>two</td>\n",
       "      <td>0.089665</td>\n",
       "      <td>0.040704</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5</th>\n",
       "      <td>bar</td>\n",
       "      <td>two</td>\n",
       "      <td>-0.336139</td>\n",
       "      <td>1.132600</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>6</th>\n",
       "      <td>foo</td>\n",
       "      <td>one</td>\n",
       "      <td>0.301063</td>\n",
       "      <td>-0.133439</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>7</th>\n",
       "      <td>foo</td>\n",
       "      <td>three</td>\n",
       "      <td>0.167332</td>\n",
       "      <td>0.789836</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "     A      B         C         D\n",
       "0  foo    one  0.024720 -1.293299\n",
       "1  bar    one  1.510969  0.509977\n",
       "2  foo    two  0.342461 -0.811380\n",
       "3  bar  three  0.227221  0.717127\n",
       "4  foo    two  0.089665  0.040704\n",
       "5  bar    two -0.336139  1.132600\n",
       "6  foo    one  0.301063 -0.133439\n",
       "7  foo  three  0.167332  0.789836"
      ]
     },
     "execution_count": 68,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df = pd.DataFrame(\n",
    "    {\n",
    "        'A': ['foo', 'bar', 'foo', 'bar', 'foo', 'bar', 'foo', 'foo'],\n",
    "        'B': ['one', 'one', 'two', 'three', 'two', 'two', 'one', 'three'],\n",
    "        'C': np.random.randn(8),\n",
    "        'D': np.random.randn(8)\n",
    "    })\n",
    "\n",
    "df"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 141
    },
    "id": "-vO5TfojS76w",
    "outputId": "3269f741-cb6e-4ecd-dc3c-b88408547813"
   },
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
       "      <th>C</th>\n",
       "      <th>D</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>A</th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>bar</th>\n",
       "      <td>1.402051</td>\n",
       "      <td>2.359705</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>foo</th>\n",
       "      <td>0.925241</td>\n",
       "      <td>-1.407579</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "            C         D\n",
       "A                      \n",
       "bar  1.402051  2.359705\n",
       "foo  0.925241 -1.407579"
      ]
     },
     "execution_count": 69,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# 생성된 데이터프레임을 그룹화한 후, 각 그룹에 sum() 함수 적용\n",
    "df.groupby('A').sum()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 263
    },
    "id": "JNauw_RfTCxR",
    "outputId": "0b92964a-e6eb-4a86-ecef-8b18600e62ee"
   },
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
       "      <th></th>\n",
       "      <th>C</th>\n",
       "      <th>D</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>A</th>\n",
       "      <th>B</th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th rowspan=\"3\" valign=\"top\">bar</th>\n",
       "      <th>one</th>\n",
       "      <td>1.510969</td>\n",
       "      <td>0.509977</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>three</th>\n",
       "      <td>0.227221</td>\n",
       "      <td>0.717127</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>two</th>\n",
       "      <td>-0.336139</td>\n",
       "      <td>1.132600</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th rowspan=\"3\" valign=\"top\">foo</th>\n",
       "      <th>one</th>\n",
       "      <td>0.325783</td>\n",
       "      <td>-1.426738</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>three</th>\n",
       "      <td>0.167332</td>\n",
       "      <td>0.789836</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>two</th>\n",
       "      <td>0.432126</td>\n",
       "      <td>-0.770676</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                  C         D\n",
       "A   B                        \n",
       "bar one    1.510969  0.509977\n",
       "    three  0.227221  0.717127\n",
       "    two   -0.336139  1.132600\n",
       "foo one    0.325783 -1.426738\n",
       "    three  0.167332  0.789836\n",
       "    two    0.432126 -0.770676"
      ]
     },
     "execution_count": 70,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# 여러 열을 기준으로 그룹화하면 계층적 인덱스가 형성, 여기에도 sum 함수 적용 가능\n",
    "df.groupby(['A', 'B']).sum()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "JbTo8lGnTP49"
   },
   "source": [
    "## **8. Reshaping**\n",
    "[- 참고: 계층적 인덱싱](https://pandas.pydata.org/pandas-docs/stable/user_guide/advanced.html), [변형](https://pandas.pydata.org/pandas-docs/stable/user_guide/reshaping.html)  \n",
    "\n",
    "### *** Stack**"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 202
    },
    "id": "RrSI8jDLTdYU",
    "outputId": "22929c0b-d173-4875-8b2a-1df0106bf54d"
   },
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
       "      <th></th>\n",
       "      <th>A</th>\n",
       "      <th>B</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>first</th>\n",
       "      <th>second</th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th rowspan=\"2\" valign=\"top\">bar</th>\n",
       "      <th>one</th>\n",
       "      <td>0.164873</td>\n",
       "      <td>-1.599363</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>two</th>\n",
       "      <td>0.262695</td>\n",
       "      <td>0.130688</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th rowspan=\"2\" valign=\"top\">baz</th>\n",
       "      <th>one</th>\n",
       "      <td>1.062799</td>\n",
       "      <td>1.995716</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>two</th>\n",
       "      <td>-1.389387</td>\n",
       "      <td>-1.260636</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                     A         B\n",
       "first second                    \n",
       "bar   one     0.164873 -1.599363\n",
       "      two     0.262695  0.130688\n",
       "baz   one     1.062799  1.995716\n",
       "      two    -1.389387 -1.260636"
      ]
     },
     "execution_count": 71,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "tuples = list(zip(*[['bar', 'bar', 'baz', 'baz',\n",
    "                     'foo', 'foo', 'qux', 'qux'],\n",
    "                    ['one', 'two', 'one', 'two',\n",
    "                     'one', 'two', 'one', 'two']]))\n",
    "\n",
    "index = pd.MultiIndex.from_tuples(tuples, names = ['first', 'second'])\n",
    "df = pd.DataFrame(np.random.randn(8, 2), index=index, columns=['A', 'B'])\n",
    "df2 = df[:4]\n",
    "df2"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/"
    },
    "id": "BhUj9FlRUFQ2",
    "outputId": "7aae188c-1230-469a-a3eb-2566f45c5074"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "first  second   \n",
       "bar    one     A    0.164873\n",
       "               B   -1.599363\n",
       "       two     A    0.262695\n",
       "               B    0.130688\n",
       "baz    one     A    1.062799\n",
       "               B    1.995716\n",
       "       two     A   -1.389387\n",
       "               B   -1.260636\n",
       "dtype: float64"
      ]
     },
     "execution_count": 72,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# stack() 메소드는 데이터프레임 열들의 계층을 압축\n",
    "stacked = df2.stack()\n",
    "stacked"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 202
    },
    "id": "Ovr1Wx5rUPg-",
    "outputId": "cee8bcf6-01a9-4b43-8220-e28245a38216"
   },
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
       "      <th></th>\n",
       "      <th>A</th>\n",
       "      <th>B</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>first</th>\n",
       "      <th>second</th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th rowspan=\"2\" valign=\"top\">bar</th>\n",
       "      <th>one</th>\n",
       "      <td>0.164873</td>\n",
       "      <td>-1.599363</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>two</th>\n",
       "      <td>0.262695</td>\n",
       "      <td>0.130688</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th rowspan=\"2\" valign=\"top\">baz</th>\n",
       "      <th>one</th>\n",
       "      <td>1.062799</td>\n",
       "      <td>1.995716</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>two</th>\n",
       "      <td>-1.389387</td>\n",
       "      <td>-1.260636</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                     A         B\n",
       "first second                    \n",
       "bar   one     0.164873 -1.599363\n",
       "      two     0.262695  0.130688\n",
       "baz   one     1.062799  1.995716\n",
       "      two    -1.389387 -1.260636"
      ]
     },
     "execution_count": 73,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# Stack된 데이터프레임 또는 MultiIndex를 인덱스로 사용하는 Series인 경우,\n",
    "# stack()의 역연산은 unstack()이며 기본적으로 마지막 계층을 unstack함\n",
    "stacked.unstack()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 202
    },
    "id": "VVLq7bAeUcbo",
    "outputId": "722a1fc7-d032-41ca-d712-2930eacf5116"
   },
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
       "      <th>second</th>\n",
       "      <th>one</th>\n",
       "      <th>two</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>first</th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th rowspan=\"2\" valign=\"top\">bar</th>\n",
       "      <th>A</th>\n",
       "      <td>0.164873</td>\n",
       "      <td>0.262695</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>B</th>\n",
       "      <td>-1.599363</td>\n",
       "      <td>0.130688</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th rowspan=\"2\" valign=\"top\">baz</th>\n",
       "      <th>A</th>\n",
       "      <td>1.062799</td>\n",
       "      <td>-1.389387</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>B</th>\n",
       "      <td>1.995716</td>\n",
       "      <td>-1.260636</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "second        one       two\n",
       "first                      \n",
       "bar   A  0.164873  0.262695\n",
       "      B -1.599363  0.130688\n",
       "baz   A  1.062799 -1.389387\n",
       "      B  1.995716 -1.260636"
      ]
     },
     "execution_count": 74,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "stacked.unstack(1)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 202
    },
    "id": "-rJjltcHUfPk",
    "outputId": "4dec8375-331b-4adb-e0cf-44e2dbe12834"
   },
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
       "      <th>first</th>\n",
       "      <th>bar</th>\n",
       "      <th>baz</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>second</th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th rowspan=\"2\" valign=\"top\">one</th>\n",
       "      <th>A</th>\n",
       "      <td>0.164873</td>\n",
       "      <td>1.062799</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>B</th>\n",
       "      <td>-1.599363</td>\n",
       "      <td>1.995716</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th rowspan=\"2\" valign=\"top\">two</th>\n",
       "      <th>A</th>\n",
       "      <td>0.262695</td>\n",
       "      <td>-1.389387</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>B</th>\n",
       "      <td>0.130688</td>\n",
       "      <td>-1.260636</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "first          bar       baz\n",
       "second                      \n",
       "one    A  0.164873  1.062799\n",
       "       B -1.599363  1.995716\n",
       "two    A  0.262695 -1.389387\n",
       "       B  0.130688 -1.260636"
      ]
     },
     "execution_count": 75,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "stacked.unstack(0)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "EFKF8WALUiB8"
   },
   "source": [
    "### *** Pivot Tables**\n",
    "[- 참고: 피봇 테이블](https://pandas.pydata.org/pandas-docs/stable/user_guide/reshaping.html)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 417
    },
    "id": "xkmPY18OUrwm",
    "outputId": "ec78f805-9d2c-4c4f-bb98-b1624777e57b"
   },
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
       "      <th>A</th>\n",
       "      <th>B</th>\n",
       "      <th>C</th>\n",
       "      <th>D</th>\n",
       "      <th>E</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>one</td>\n",
       "      <td>A</td>\n",
       "      <td>foo</td>\n",
       "      <td>-0.335507</td>\n",
       "      <td>0.728239</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>one</td>\n",
       "      <td>B</td>\n",
       "      <td>foo</td>\n",
       "      <td>-0.251893</td>\n",
       "      <td>1.290054</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>two</td>\n",
       "      <td>C</td>\n",
       "      <td>foo</td>\n",
       "      <td>0.590448</td>\n",
       "      <td>0.226098</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>three</td>\n",
       "      <td>A</td>\n",
       "      <td>bar</td>\n",
       "      <td>1.207361</td>\n",
       "      <td>0.915646</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>one</td>\n",
       "      <td>B</td>\n",
       "      <td>bar</td>\n",
       "      <td>0.296306</td>\n",
       "      <td>-1.981152</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5</th>\n",
       "      <td>one</td>\n",
       "      <td>C</td>\n",
       "      <td>bar</td>\n",
       "      <td>0.166610</td>\n",
       "      <td>-0.312002</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>6</th>\n",
       "      <td>two</td>\n",
       "      <td>A</td>\n",
       "      <td>foo</td>\n",
       "      <td>1.505633</td>\n",
       "      <td>-0.791708</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>7</th>\n",
       "      <td>three</td>\n",
       "      <td>B</td>\n",
       "      <td>foo</td>\n",
       "      <td>-1.978302</td>\n",
       "      <td>-1.671514</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>8</th>\n",
       "      <td>one</td>\n",
       "      <td>C</td>\n",
       "      <td>foo</td>\n",
       "      <td>1.263163</td>\n",
       "      <td>-2.340603</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>9</th>\n",
       "      <td>one</td>\n",
       "      <td>A</td>\n",
       "      <td>bar</td>\n",
       "      <td>-0.028701</td>\n",
       "      <td>-1.374556</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>10</th>\n",
       "      <td>two</td>\n",
       "      <td>B</td>\n",
       "      <td>bar</td>\n",
       "      <td>0.657087</td>\n",
       "      <td>0.272042</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>11</th>\n",
       "      <td>three</td>\n",
       "      <td>C</td>\n",
       "      <td>bar</td>\n",
       "      <td>0.351417</td>\n",
       "      <td>1.455815</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "        A  B    C         D         E\n",
       "0     one  A  foo -0.335507  0.728239\n",
       "1     one  B  foo -0.251893  1.290054\n",
       "2     two  C  foo  0.590448  0.226098\n",
       "3   three  A  bar  1.207361  0.915646\n",
       "4     one  B  bar  0.296306 -1.981152\n",
       "5     one  C  bar  0.166610 -0.312002\n",
       "6     two  A  foo  1.505633 -0.791708\n",
       "7   three  B  foo -1.978302 -1.671514\n",
       "8     one  C  foo  1.263163 -2.340603\n",
       "9     one  A  bar -0.028701 -1.374556\n",
       "10    two  B  bar  0.657087  0.272042\n",
       "11  three  C  bar  0.351417  1.455815"
      ]
     },
     "execution_count": 76,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df = pd.DataFrame({'A': ['one', 'one', 'two', 'three'] * 3,\n",
    "                   'B': ['A', 'B', 'C'] * 4,\n",
    "                   'C': ['foo', 'foo', 'foo', 'bar', 'bar', 'bar'] * 2,\n",
    "                   'D': np.random.randn(12),\n",
    "                   'E': np.random.randn(12)})\n",
    "\n",
    "df"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 355
    },
    "id": "OX6L958BVGEP",
    "outputId": "f101f290-fc45-46b9-a2a4-51966e167ee7"
   },
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
       "      <th>C</th>\n",
       "      <th>bar</th>\n",
       "      <th>foo</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>A</th>\n",
       "      <th>B</th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th rowspan=\"3\" valign=\"top\">one</th>\n",
       "      <th>A</th>\n",
       "      <td>-0.028701</td>\n",
       "      <td>-0.335507</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>B</th>\n",
       "      <td>0.296306</td>\n",
       "      <td>-0.251893</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>C</th>\n",
       "      <td>0.166610</td>\n",
       "      <td>1.263163</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th rowspan=\"3\" valign=\"top\">three</th>\n",
       "      <th>A</th>\n",
       "      <td>1.207361</td>\n",
       "      <td>NaN</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>B</th>\n",
       "      <td>NaN</td>\n",
       "      <td>-1.978302</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>C</th>\n",
       "      <td>0.351417</td>\n",
       "      <td>NaN</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th rowspan=\"3\" valign=\"top\">two</th>\n",
       "      <th>A</th>\n",
       "      <td>NaN</td>\n",
       "      <td>1.505633</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>B</th>\n",
       "      <td>0.657087</td>\n",
       "      <td>NaN</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>C</th>\n",
       "      <td>NaN</td>\n",
       "      <td>0.590448</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "C             bar       foo\n",
       "A     B                    \n",
       "one   A -0.028701 -0.335507\n",
       "      B  0.296306 -0.251893\n",
       "      C  0.166610  1.263163\n",
       "three A  1.207361       NaN\n",
       "      B       NaN -1.978302\n",
       "      C  0.351417       NaN\n",
       "two   A       NaN  1.505633\n",
       "      B  0.657087       NaN\n",
       "      C       NaN  0.590448"
      ]
     },
     "execution_count": 77,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# 피봇 테이블 생성\n",
    "pd.pivot_table(df, values='D', index=['A', 'B'], columns=['C'])"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "fEonaQ6tVYAa"
   },
   "source": [
    "## **9. Time Series**\n",
    "Pandas는 자주 일어나는 변환(ex. 5분마다 일어나는 데이터의 2차 데이터 변환) 사이에 수행하는 리샘플링 연산을 위해 간단하고 강력하고 효율적인 함수를 제공한다.  \n",
    "재무(금융) 응용에서 매우 일반적이나 이에 국한되지는 않는다.  \n",
    "[- 참고: 시계열](https://pandas.pydata.org/pandas-docs/stable/user_guide/timeseries.html)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "id": "TVU5S6lUYnTa"
   },
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/"
    },
    "id": "sme5BveBYRF0",
    "outputId": "407ea609-507d-4b2a-f4ee-fec63d7f6234"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "2012-01-01    25049\n",
       "Freq: 5T, dtype: int64"
      ]
     },
     "execution_count": 78,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "rng = pd.date_range('1/1/2012', periods=100, freq='S')\n",
    "ts = pd.Series(np.random.randint(0, 500, len(rng)), index=rng)\n",
    "ts.resample('5Min').sum()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/"
    },
    "id": "hngc6xo2YfbR",
    "outputId": "c374b119-96d4-4bfc-c007-9f4de042e366"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "2012-03-06    0.099699\n",
       "2012-03-07    0.235671\n",
       "2012-03-08    0.636022\n",
       "2012-03-09   -1.993396\n",
       "2012-03-10   -0.113581\n",
       "Freq: D, dtype: float64"
      ]
     },
     "execution_count": 79,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# 시간대 표현\n",
    "rng = pd.date_range('3/6/2012 00:00', periods=5, freq='D')\n",
    "ts = pd.Series(np.random.randn(len(rng)), rng)\n",
    "ts"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/"
    },
    "id": "3NynKQRLY80D",
    "outputId": "c59cad2f-505a-4e08-e545-7def518777db"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "2012-03-06 00:00:00+00:00    0.099699\n",
       "2012-03-07 00:00:00+00:00    0.235671\n",
       "2012-03-08 00:00:00+00:00    0.636022\n",
       "2012-03-09 00:00:00+00:00   -1.993396\n",
       "2012-03-10 00:00:00+00:00   -0.113581\n",
       "Freq: D, dtype: float64"
      ]
     },
     "execution_count": 80,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "ts_utc = ts.tz_localize('UTC')\n",
    "ts_utc"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/"
    },
    "id": "ML6dWdmjZM97",
    "outputId": "1983951e-6c8c-4a0c-93e0-01c09b1bbb05"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "2012-03-05 19:00:00-05:00    0.099699\n",
       "2012-03-06 19:00:00-05:00    0.235671\n",
       "2012-03-07 19:00:00-05:00    0.636022\n",
       "2012-03-08 19:00:00-05:00   -1.993396\n",
       "2012-03-09 19:00:00-05:00   -0.113581\n",
       "Freq: D, dtype: float64"
      ]
     },
     "execution_count": 81,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# 다른 시간대로 변환\n",
    "ts_utc.tz_convert('US/Eastern')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/"
    },
    "id": "G9e0BSSAZSbg",
    "outputId": "7b862b6d-ce1f-4e5c-ba92-abd31ebed8ee"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "2012-01-31   -1.161855\n",
       "2012-02-29    0.262081\n",
       "2012-03-31    0.238179\n",
       "2012-04-30   -1.160233\n",
       "2012-05-31    0.816160\n",
       "Freq: M, dtype: float64"
      ]
     },
     "execution_count": 82,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# 시간 표현 ↔ 기간 표현 변환\n",
    "rng = pd.date_range('1/1/2012', periods=5, freq='M')\n",
    "ts = pd.Series(np.random.randn(len(rng)), index=rng)\n",
    "ts"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/"
    },
    "id": "KYW5eUKXZv9O",
    "outputId": "5ed6d0fe-2c81-4709-996c-30d34636cd7a"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "2012-01   -1.161855\n",
       "2012-02    0.262081\n",
       "2012-03    0.238179\n",
       "2012-04   -1.160233\n",
       "2012-05    0.816160\n",
       "Freq: M, dtype: float64"
      ]
     },
     "execution_count": 83,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "ps = ts.to_period()\n",
    "ps"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/"
    },
    "id": "mlN4V4sSZyvl",
    "outputId": "8a346541-f031-46ce-de3f-24e0fae11e89"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "2012-01-01   -1.161855\n",
       "2012-02-01    0.262081\n",
       "2012-03-01    0.238179\n",
       "2012-04-01   -1.160233\n",
       "2012-05-01    0.816160\n",
       "Freq: MS, dtype: float64"
      ]
     },
     "execution_count": 84,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "ps.to_timestamp()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "TGd6CDcgZ2Yl"
   },
   "source": [
    "기간 ↔ 시간 변환은 편리한 산술 기능을 사용할 수 있도록 만든다.  \n",
    "11월에 끝나는 연말 결산의 분기별 빈도를, 분기말 익월의 월말일 오전 9시로 변환해보자."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/"
    },
    "id": "N8UgOdaIZ_tX",
    "outputId": "d5bfc70d-df24-461f-fcf7-db1e673df7a5"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "1990-03-01 00:00    0.671614\n",
       "1990-06-01 00:00   -0.141739\n",
       "1990-09-01 00:00    0.070749\n",
       "1990-12-01 00:00   -0.769261\n",
       "1991-03-01 00:00   -0.432595\n",
       "Freq: H, dtype: float64"
      ]
     },
     "execution_count": 85,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "prng = pd.period_range('1990Q1', '2000Q4', freq='Q-NOV')\n",
    "ts = pd.Series(np.random.randn(len(prng)), prng)\n",
    "ts.index = (prng.asfreq('M', 'e') + 1).asfreq('H', 'S')\n",
    "ts.head()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "Gpd4f-lG_HUu"
   },
   "source": [
    "## **10. Categoricals**\n",
    "Pandas는 데이터프레임 내에 범주형 데이터를 포함할 수 있다.  \n",
    "[- 참고: 범주형 소개](https://pandas.pydata.org/pandas-docs/stable/user_guide/categorical.html), [API 문서](https://pandas.pydata.org/pandas-docs/stable/reference/index.html)  "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "id": "iPpzJzwB_W8y"
   },
   "outputs": [],
   "source": [
    "df = pd.DataFrame({\"id\":[1,2,3,4,5,6], \"raw_grade\":['a', 'b', 'b', 'a', 'a', 'e']})"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "IYg4v9OY_kfr"
   },
   "source": [
    "가공하지 않은 성적을 범주형 데이터로 변환한다."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/"
    },
    "id": "Or8nA9h2_vbO",
    "outputId": "747393b8-13c9-4c40-f83d-7f366a694cbd"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0    a\n",
       "1    b\n",
       "2    b\n",
       "3    a\n",
       "4    a\n",
       "5    e\n",
       "Name: grade, dtype: category\n",
       "Categories (3, object): ['a', 'b', 'e']"
      ]
     },
     "execution_count": 87,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df[\"grade\"] = df[\"raw_grade\"].astype(\"category\")\n",
    "df[\"grade\"]"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "e11XnHXX_2nA"
   },
   "source": [
    "범주에 더 의미있는 이름을 붙이자. (Series.cat.categories로 할당하는 것이 적합)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "id": "FmH8iW2B_-T4"
   },
   "outputs": [],
   "source": [
    "df[\"grade\"].cat.categories = [\"very good\", \"good\", \"very bad\"]"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "9AFdJfT5ADTk"
   },
   "source": [
    "범주 순서를 바꾸고 동시에 누락된 범주를 추가한다. (Series.cat에 속하는 메소드는 기본적으로 새로운 Series를 반환)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/"
    },
    "id": "BaXTpCO_AJrC",
    "outputId": "695f4ed7-d1fb-422a-d57b-efefe880516d"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0    very good\n",
       "1         good\n",
       "2         good\n",
       "3    very good\n",
       "4    very good\n",
       "5     very bad\n",
       "Name: grade, dtype: category\n",
       "Categories (5, object): ['very bad', 'bad', 'medium', 'good', 'very good']"
      ]
     },
     "execution_count": 89,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df[\"grade\"] = df[\"grade\"].cat.set_categories([\"very bad\", \"bad\", \"medium\", \"good\", \"very good\"])\n",
    "df[\"grade\"]"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "fpH1r8daAUis"
   },
   "source": [
    "정렬은 사전 순서가 아니라, 해당 범주에서 지정된 순서대로 배열한다."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 233
    },
    "id": "06mNxH6u0pok",
    "outputId": "7b37c179-e9d6-42f3-92a0-9b4ad92a8f40"
   },
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
       "      <th>id</th>\n",
       "      <th>raw_grade</th>\n",
       "      <th>grade</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>5</th>\n",
       "      <td>6</td>\n",
       "      <td>e</td>\n",
       "      <td>very bad</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>2</td>\n",
       "      <td>b</td>\n",
       "      <td>good</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>3</td>\n",
       "      <td>b</td>\n",
       "      <td>good</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>1</td>\n",
       "      <td>a</td>\n",
       "      <td>very good</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>4</td>\n",
       "      <td>a</td>\n",
       "      <td>very good</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>5</td>\n",
       "      <td>a</td>\n",
       "      <td>very good</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   id raw_grade      grade\n",
       "5   6         e   very bad\n",
       "1   2         b       good\n",
       "2   3         b       good\n",
       "0   1         a  very good\n",
       "3   4         a  very good\n",
       "4   5         a  very good"
      ]
     },
     "execution_count": 90,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.sort_values(by=\"grade\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "OJOTt17I0txu"
   },
   "source": [
    "범주의 열을 기준으로 그룹화하면 빈 범주도 표시된다."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/"
    },
    "id": "UjxHCQJm0y-K",
    "outputId": "27e3b143-137f-4090-8152-02bea5f8023f"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "grade\n",
       "very bad     1\n",
       "bad          0\n",
       "medium       0\n",
       "good         2\n",
       "very good    3\n",
       "dtype: int64"
      ]
     },
     "execution_count": 92,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.groupby(\"grade\").size()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "HaCRMKcv06rJ"
   },
   "source": [
    "## **11. Plotting**\n",
    "[- 참고: Plotting](https://pandas.pydata.org/pandas-docs/stable/user_guide/visualization.html)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/"
    },
    "id": "P7HiqEm71Ed0",
    "outputId": "fa374a5a-ea56-4c1f-d9fa-a2e52aedf97e"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<pandas.plotting._core.PlotAccessor object at 0x7f4670f2ae80>"
      ]
     },
     "execution_count": 93,
     "metadata": {
      "tags": []
     },
     "output_type": "execute_result"
    }
   ],
   "source": [
    "ts = pd.Series(np.random.randn(1000), index=pd.date_range('1/1/2000', periods=1000))\n",
    "ts = ts.cumsum()\n",
    "ts.plot"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "qKSf3_Ko1Ofi"
   },
   "source": [
    "데이터프레임에서 plot() 메소드는 라벨이 존재하는 모든 열을 그릴 때 편리하다."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 363
    },
    "id": "TJ5xt-WY1Xbm",
    "outputId": "c6fe351a-8ef9-40d2-931f-51e6f941493c"
   },
   "outputs": [
    {
     "ename": "AttributeError",
     "evalue": "ignored",
     "output_type": "error",
     "traceback": [
      "\u001b[0;31m---------------------------------------------------------------------------\u001b[0m",
      "\u001b[0;31mAttributeError\u001b[0m                            Traceback (most recent call last)",
      "\u001b[0;32m<ipython-input-97-bc219ebae1fe>\u001b[0m in \u001b[0;36m<module>\u001b[0;34m()\u001b[0m\n\u001b[0;32m----> 1\u001b[0;31m df = pd.DataFrame(np.random.randn(1000, 4), index=ts.index,\n\u001b[0m\u001b[1;32m      2\u001b[0m                   columns=['A', 'B', 'C', 'D'])  \n\u001b[1;32m      3\u001b[0m \u001b[0mdf\u001b[0m \u001b[0;34m=\u001b[0m \u001b[0mdf\u001b[0m\u001b[0;34m.\u001b[0m\u001b[0mcumsum\u001b[0m\u001b[0;34m(\u001b[0m\u001b[0;34m)\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[1;32m      4\u001b[0m \u001b[0mplt\u001b[0m\u001b[0;34m.\u001b[0m\u001b[0mfigure\u001b[0m\u001b[0;34m(\u001b[0m\u001b[0;34m)\u001b[0m\u001b[0;34m;\u001b[0m \u001b[0mdf\u001b[0m\u001b[0;34m.\u001b[0m\u001b[0mplot\u001b[0m\u001b[0;34m(\u001b[0m\u001b[0;34m)\u001b[0m\u001b[0;34m;\u001b[0m \u001b[0mplt\u001b[0m\u001b[0;34m.\u001b[0m\u001b[0mlegend\u001b[0m\u001b[0;34m(\u001b[0m\u001b[0mloc\u001b[0m\u001b[0;34m=\u001b[0m\u001b[0;34m'best'\u001b[0m\u001b[0;34m)\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n",
      "\u001b[0;32m/usr/local/lib/python3.6/dist-packages/pandas/core/generic.py\u001b[0m in \u001b[0;36m__getattr__\u001b[0;34m(self, name)\u001b[0m\n\u001b[1;32m   5137\u001b[0m             \u001b[0;32mif\u001b[0m \u001b[0mself\u001b[0m\u001b[0;34m.\u001b[0m\u001b[0m_info_axis\u001b[0m\u001b[0;34m.\u001b[0m\u001b[0m_can_hold_identifiers_and_holds_name\u001b[0m\u001b[0;34m(\u001b[0m\u001b[0mname\u001b[0m\u001b[0;34m)\u001b[0m\u001b[0;34m:\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[1;32m   5138\u001b[0m                 \u001b[0;32mreturn\u001b[0m \u001b[0mself\u001b[0m\u001b[0;34m[\u001b[0m\u001b[0mname\u001b[0m\u001b[0;34m]\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[0;32m-> 5139\u001b[0;31m             \u001b[0;32mreturn\u001b[0m \u001b[0mobject\u001b[0m\u001b[0;34m.\u001b[0m\u001b[0m__getattribute__\u001b[0m\u001b[0;34m(\u001b[0m\u001b[0mself\u001b[0m\u001b[0;34m,\u001b[0m \u001b[0mname\u001b[0m\u001b[0;34m)\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[0m\u001b[1;32m   5140\u001b[0m \u001b[0;34m\u001b[0m\u001b[0m\n\u001b[1;32m   5141\u001b[0m     \u001b[0;32mdef\u001b[0m \u001b[0m__setattr__\u001b[0m\u001b[0;34m(\u001b[0m\u001b[0mself\u001b[0m\u001b[0;34m,\u001b[0m \u001b[0mname\u001b[0m\u001b[0;34m:\u001b[0m \u001b[0mstr\u001b[0m\u001b[0;34m,\u001b[0m \u001b[0mvalue\u001b[0m\u001b[0;34m)\u001b[0m \u001b[0;34m->\u001b[0m \u001b[0;32mNone\u001b[0m\u001b[0;34m:\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n",
      "\u001b[0;31mAttributeError\u001b[0m: 'DataFrame' object has no attribute 'DataFrame'"
     ]
    }
   ],
   "source": [
    "df = pd.DataFrame(np.random.randn(1000, 4), index=ts.index,\n",
    "                  columns=['A', 'B', 'C', 'D'])  \n",
    "df = df.cumsum()\n",
    "plt.figure(); df.plot(); plt.legend(loc='best')"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "ryWktYkM17PT"
   },
   "source": [
    "## **12. Getting Data In / Out**\n",
    "\n",
    "### **CSV**\n",
    "csv 파일에 쓴다.  \n",
    "df.to_csv('foo.csv')  \n",
    "\n",
    "csv 파일을 읽는다.  \n",
    "pd.read_csv('foo.csv')\n",
    "\n",
    "### **HDF5**\n",
    "HDF5 Store에 쓴다.  \n",
    "df.to_hdf('foo.h5','df')  \n",
    "HDF5 Store에서 읽는다.  \n",
    "pd.read_hdf('foo.h5','df')  \n",
    "\n",
    "### **Excel**\n",
    "엑셀 파일에 쓴다.  \n",
    "df.to_excel('foo.xlsx', sheet_name='Sheet1')  \n",
    "엑셀 파일을 읽는다.  \n",
    "pd.read_excel('foo.xlsx', 'Sheet1', index_col=None, na_values=['NA'])  "
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "OU3-CZPo22_D"
   },
   "source": [
    "## **13. Gotchas**\n",
    "연산 수행 시, 다음과 같은 예외 상황이 나타날 수 있다."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {
     "base_uri": "https://localhost:8080/",
     "height": 325
    },
    "id": "0z_zRERH28Uo",
    "outputId": "797310bb-65be-4def-dbca-ff93e9c94782"
   },
   "outputs": [
    {
     "ename": "AttributeError",
     "evalue": "ignored",
     "output_type": "error",
     "traceback": [
      "\u001b[0;31m---------------------------------------------------------------------------\u001b[0m",
      "\u001b[0;31mAttributeError\u001b[0m                            Traceback (most recent call last)",
      "\u001b[0;32m<ipython-input-104-06fa23a4b3e2>\u001b[0m in \u001b[0;36m<module>\u001b[0;34m()\u001b[0m\n\u001b[0;32m----> 1\u001b[0;31m \u001b[0;32mif\u001b[0m \u001b[0mpd\u001b[0m\u001b[0;34m.\u001b[0m\u001b[0mSeries\u001b[0m\u001b[0;34m(\u001b[0m\u001b[0;34m[\u001b[0m\u001b[0;32mFalse\u001b[0m\u001b[0;34m,\u001b[0m \u001b[0;32mTrue\u001b[0m\u001b[0;34m,\u001b[0m \u001b[0;32mFalse\u001b[0m\u001b[0;34m]\u001b[0m\u001b[0;34m)\u001b[0m\u001b[0;34m:\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[0m\u001b[1;32m      2\u001b[0m   \u001b[0mprint\u001b[0m\u001b[0;34m(\u001b[0m\u001b[0;34m\"I was true\"\u001b[0m\u001b[0;34m)\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n",
      "\u001b[0;32m/usr/local/lib/python3.6/dist-packages/pandas/core/generic.py\u001b[0m in \u001b[0;36m__getattr__\u001b[0;34m(self, name)\u001b[0m\n\u001b[1;32m   5137\u001b[0m             \u001b[0;32mif\u001b[0m \u001b[0mself\u001b[0m\u001b[0;34m.\u001b[0m\u001b[0m_info_axis\u001b[0m\u001b[0;34m.\u001b[0m\u001b[0m_can_hold_identifiers_and_holds_name\u001b[0m\u001b[0;34m(\u001b[0m\u001b[0mname\u001b[0m\u001b[0;34m)\u001b[0m\u001b[0;34m:\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[1;32m   5138\u001b[0m                 \u001b[0;32mreturn\u001b[0m \u001b[0mself\u001b[0m\u001b[0;34m[\u001b[0m\u001b[0mname\u001b[0m\u001b[0;34m]\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[0;32m-> 5139\u001b[0;31m             \u001b[0;32mreturn\u001b[0m \u001b[0mobject\u001b[0m\u001b[0;34m.\u001b[0m\u001b[0m__getattribute__\u001b[0m\u001b[0;34m(\u001b[0m\u001b[0mself\u001b[0m\u001b[0;34m,\u001b[0m \u001b[0mname\u001b[0m\u001b[0;34m)\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[0m\u001b[1;32m   5140\u001b[0m \u001b[0;34m\u001b[0m\u001b[0m\n\u001b[1;32m   5141\u001b[0m     \u001b[0;32mdef\u001b[0m \u001b[0m__setattr__\u001b[0m\u001b[0;34m(\u001b[0m\u001b[0mself\u001b[0m\u001b[0;34m,\u001b[0m \u001b[0mname\u001b[0m\u001b[0;34m:\u001b[0m \u001b[0mstr\u001b[0m\u001b[0;34m,\u001b[0m \u001b[0mvalue\u001b[0m\u001b[0;34m)\u001b[0m \u001b[0;34m->\u001b[0m \u001b[0;32mNone\u001b[0m\u001b[0;34m:\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n",
      "\u001b[0;31mAttributeError\u001b[0m: 'DataFrame' object has no attribute 'Series'"
     ]
    }
   ],
   "source": [
    "if pd.Series([False, True, False]):\n",
    "  print(\"I was true\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "1GXYqOHT3CWV"
   },
   "source": [
    "이러한 경우에는 any(), all(), empty 등을 사용해서 무엇을 원하는지를 선택해주어야 한다.  \n",
    "```python\n",
    "if pd.Series([False, True, False]) is not None:\n",
    "      print(\"I was not None\")\n",
    "```"
   ]
  }
 ],
 "metadata": {
  "colab": {
   "collapsed_sections": [],
   "name": "Pandas 10분 완성.ipynb",
   "provenance": []
  },
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
   "version": "3.8.3"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 1
}
