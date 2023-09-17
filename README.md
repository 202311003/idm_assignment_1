{
  "cells": [
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "view-in-github",
        "colab_type": "text"
      },
      "source": [
        "<a href=\"https://colab.research.google.com/github/202311003/idm_assignment_1/blob/202311071/README.md\" target=\"_parent\"><img src=\"https://colab.research.google.com/assets/colab-badge.svg\" alt=\"Open In Colab\"/></a>"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "uNrzrxlnOZn9"
      },
      "source": [
        "#1.Setting up the directory"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 8,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "pD0iptOaEeq5",
        "outputId": "cf2b0b51-bc1f-4468-a122-26afdd4a5664"
      },
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "mkdir: cannot create directory ‘data’: File exists\n"
          ]
        }
      ],
      "source": [
        "!mkdir data"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 9,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "xZv8ghAcdNim",
        "outputId": "f0807b62-faad-4ef3-c5bc-7bcc9b66b724"
      },
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "Archive:  data/archive.zip\n",
            "replace data/the weather of 155 countries in 2020.csv? [y]es, [n]o, [A]ll, [N]one, [r]ename: N\n"
          ]
        }
      ],
      "source": [
        "!unzip data/archive.zip -d data/"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "0WqB8uJMOUl0"
      },
      "source": [
        "#2.EDA"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 11,
      "metadata": {
        "id": "m1ig5rsE1s0U"
      },
      "outputs": [],
      "source": [
        "import math\n",
        "import numpy as np\n",
        "import pandas as pd\n",
        "\n",
        "import matplotlib.pyplot as plt\n",
        "import seaborn as sns"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 12,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 377
        },
        "id": "vYSzXzQU10af",
        "outputId": "a7670e1d-21b3-47ea-cae3-53003bcfa71c"
      },
      "outputs": [
        {
          "output_type": "stream",
          "name": "stderr",
          "text": [
            "<ipython-input-12-692c75a706a3>:1: DtypeWarning: Columns (16,17,18,19,23) have mixed types. Specify dtype option on import or set low_memory=False.\n",
            "  df = pd.read_csv('data/the weather of 187 countries in 2020.csv')\n"
          ]
        },
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "       STATION Country/Region        DATE  Year  Month  Day  PRCP  SNWD  TAVG  \\\n",
              "0  TZ000063894        Comoros  2020-01-22  2020      1   22  10.9   NaN  27.6   \n",
              "1  TZ000063894        Comoros  2020-01-23  2020      1   23   0.0   NaN  26.7   \n",
              "2  TZ000063894        Comoros  2020-01-24  2020      1   24   9.4   NaN  27.9   \n",
              "3  TZ000063894        Comoros  2020-01-25  2020      1   25   0.3   NaN  27.9   \n",
              "4  TZ000063894        Comoros  2020-01-26  2020      1   26   0.0   NaN  28.2   \n",
              "\n",
              "   TMAX  ...  LONGITUDE  ELEVATION  PRCP_ATTRIBUTES  TAVG_ATTRIBUTES  \\\n",
              "0  30.2  ...        NaN        NaN              NaN              NaN   \n",
              "1   NaN  ...        NaN        NaN              NaN              NaN   \n",
              "2  30.6  ...        NaN        NaN              NaN              NaN   \n",
              "3  30.2  ...        NaN        NaN              NaN              NaN   \n",
              "4  31.5  ...        NaN        NaN              NaN              NaN   \n",
              "\n",
              "   TMAX_ATTRIBUTES TMIN_ATTRIBUTES DAPR MDPR WESD  SNWD_ATTRIBUTES  \n",
              "0              NaN             NaN  NaN  NaN  NaN              NaN  \n",
              "1              NaN             NaN  NaN  NaN  NaN              NaN  \n",
              "2              NaN             NaN  NaN  NaN  NaN              NaN  \n",
              "3              NaN             NaN  NaN  NaN  NaN              NaN  \n",
              "4              NaN             NaN  NaN  NaN  NaN              NaN  \n",
              "\n",
              "[5 rows x 23 columns]"
            ],
            "text/html": [
              "\n",
              "  <div id=\"df-c168840d-a373-44bc-a919-2adb69700a0d\" class=\"colab-df-container\">\n",
              "    <div>\n",
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
              "      <th>STATION</th>\n",
              "      <th>Country/Region</th>\n",
              "      <th>DATE</th>\n",
              "      <th>Year</th>\n",
              "      <th>Month</th>\n",
              "      <th>Day</th>\n",
              "      <th>PRCP</th>\n",
              "      <th>SNWD</th>\n",
              "      <th>TAVG</th>\n",
              "      <th>TMAX</th>\n",
              "      <th>...</th>\n",
              "      <th>LONGITUDE</th>\n",
              "      <th>ELEVATION</th>\n",
              "      <th>PRCP_ATTRIBUTES</th>\n",
              "      <th>TAVG_ATTRIBUTES</th>\n",
              "      <th>TMAX_ATTRIBUTES</th>\n",
              "      <th>TMIN_ATTRIBUTES</th>\n",
              "      <th>DAPR</th>\n",
              "      <th>MDPR</th>\n",
              "      <th>WESD</th>\n",
              "      <th>SNWD_ATTRIBUTES</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>0</th>\n",
              "      <td>TZ000063894</td>\n",
              "      <td>Comoros</td>\n",
              "      <td>2020-01-22</td>\n",
              "      <td>2020</td>\n",
              "      <td>1</td>\n",
              "      <td>22</td>\n",
              "      <td>10.9</td>\n",
              "      <td>NaN</td>\n",
              "      <td>27.6</td>\n",
              "      <td>30.2</td>\n",
              "      <td>...</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>1</th>\n",
              "      <td>TZ000063894</td>\n",
              "      <td>Comoros</td>\n",
              "      <td>2020-01-23</td>\n",
              "      <td>2020</td>\n",
              "      <td>1</td>\n",
              "      <td>23</td>\n",
              "      <td>0.0</td>\n",
              "      <td>NaN</td>\n",
              "      <td>26.7</td>\n",
              "      <td>NaN</td>\n",
              "      <td>...</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2</th>\n",
              "      <td>TZ000063894</td>\n",
              "      <td>Comoros</td>\n",
              "      <td>2020-01-24</td>\n",
              "      <td>2020</td>\n",
              "      <td>1</td>\n",
              "      <td>24</td>\n",
              "      <td>9.4</td>\n",
              "      <td>NaN</td>\n",
              "      <td>27.9</td>\n",
              "      <td>30.6</td>\n",
              "      <td>...</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>3</th>\n",
              "      <td>TZ000063894</td>\n",
              "      <td>Comoros</td>\n",
              "      <td>2020-01-25</td>\n",
              "      <td>2020</td>\n",
              "      <td>1</td>\n",
              "      <td>25</td>\n",
              "      <td>0.3</td>\n",
              "      <td>NaN</td>\n",
              "      <td>27.9</td>\n",
              "      <td>30.2</td>\n",
              "      <td>...</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>4</th>\n",
              "      <td>TZ000063894</td>\n",
              "      <td>Comoros</td>\n",
              "      <td>2020-01-26</td>\n",
              "      <td>2020</td>\n",
              "      <td>1</td>\n",
              "      <td>26</td>\n",
              "      <td>0.0</td>\n",
              "      <td>NaN</td>\n",
              "      <td>28.2</td>\n",
              "      <td>31.5</td>\n",
              "      <td>...</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "      <td>NaN</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "<p>5 rows × 23 columns</p>\n",
              "</div>\n",
              "    <div class=\"colab-df-buttons\">\n",
              "\n",
              "  <div class=\"colab-df-container\">\n",
              "    <button class=\"colab-df-convert\" onclick=\"convertToInteractive('df-c168840d-a373-44bc-a919-2adb69700a0d')\"\n",
              "            title=\"Convert this dataframe to an interactive table.\"\n",
              "            style=\"display:none;\">\n",
              "\n",
              "  <svg xmlns=\"http://www.w3.org/2000/svg\" height=\"24px\" viewBox=\"0 -960 960 960\">\n",
              "    <path d=\"M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z\"/>\n",
              "  </svg>\n",
              "    </button>\n",
              "\n",
              "  <style>\n",
              "    .colab-df-container {\n",
              "      display:flex;\n",
              "      gap: 12px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert {\n",
              "      background-color: #E8F0FE;\n",
              "      border: none;\n",
              "      border-radius: 50%;\n",
              "      cursor: pointer;\n",
              "      display: none;\n",
              "      fill: #1967D2;\n",
              "      height: 32px;\n",
              "      padding: 0 0 0 0;\n",
              "      width: 32px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert:hover {\n",
              "      background-color: #E2EBFA;\n",
              "      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);\n",
              "      fill: #174EA6;\n",
              "    }\n",
              "\n",
              "    .colab-df-buttons div {\n",
              "      margin-bottom: 4px;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert {\n",
              "      background-color: #3B4455;\n",
              "      fill: #D2E3FC;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert:hover {\n",
              "      background-color: #434B5C;\n",
              "      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);\n",
              "      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));\n",
              "      fill: #FFFFFF;\n",
              "    }\n",
              "  </style>\n",
              "\n",
              "    <script>\n",
              "      const buttonEl =\n",
              "        document.querySelector('#df-c168840d-a373-44bc-a919-2adb69700a0d button.colab-df-convert');\n",
              "      buttonEl.style.display =\n",
              "        google.colab.kernel.accessAllowed ? 'block' : 'none';\n",
              "\n",
              "      async function convertToInteractive(key) {\n",
              "        const element = document.querySelector('#df-c168840d-a373-44bc-a919-2adb69700a0d');\n",
              "        const dataTable =\n",
              "          await google.colab.kernel.invokeFunction('convertToInteractive',\n",
              "                                                    [key], {});\n",
              "        if (!dataTable) return;\n",
              "\n",
              "        const docLinkHtml = 'Like what you see? Visit the ' +\n",
              "          '<a target=\"_blank\" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'\n",
              "          + ' to learn more about interactive tables.';\n",
              "        element.innerHTML = '';\n",
              "        dataTable['output_type'] = 'display_data';\n",
              "        await google.colab.output.renderOutput(dataTable, element);\n",
              "        const docLink = document.createElement('div');\n",
              "        docLink.innerHTML = docLinkHtml;\n",
              "        element.appendChild(docLink);\n",
              "      }\n",
              "    </script>\n",
              "  </div>\n",
              "\n",
              "\n",
              "<div id=\"df-1d612e51-235b-467a-8fb4-d8488f7bf6cd\">\n",
              "  <button class=\"colab-df-quickchart\" onclick=\"quickchart('df-1d612e51-235b-467a-8fb4-d8488f7bf6cd')\"\n",
              "            title=\"Suggest charts.\"\n",
              "            style=\"display:none;\">\n",
              "\n",
              "<svg xmlns=\"http://www.w3.org/2000/svg\" height=\"24px\"viewBox=\"0 0 24 24\"\n",
              "     width=\"24px\">\n",
              "    <g>\n",
              "        <path d=\"M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zM9 17H7v-7h2v7zm4 0h-2V7h2v10zm4 0h-2v-4h2v4z\"/>\n",
              "    </g>\n",
              "</svg>\n",
              "  </button>\n",
              "\n",
              "<style>\n",
              "  .colab-df-quickchart {\n",
              "      --bg-color: #E8F0FE;\n",
              "      --fill-color: #1967D2;\n",
              "      --hover-bg-color: #E2EBFA;\n",
              "      --hover-fill-color: #174EA6;\n",
              "      --disabled-fill-color: #AAA;\n",
              "      --disabled-bg-color: #DDD;\n",
              "  }\n",
              "\n",
              "  [theme=dark] .colab-df-quickchart {\n",
              "      --bg-color: #3B4455;\n",
              "      --fill-color: #D2E3FC;\n",
              "      --hover-bg-color: #434B5C;\n",
              "      --hover-fill-color: #FFFFFF;\n",
              "      --disabled-bg-color: #3B4455;\n",
              "      --disabled-fill-color: #666;\n",
              "  }\n",
              "\n",
              "  .colab-df-quickchart {\n",
              "    background-color: var(--bg-color);\n",
              "    border: none;\n",
              "    border-radius: 50%;\n",
              "    cursor: pointer;\n",
              "    display: none;\n",
              "    fill: var(--fill-color);\n",
              "    height: 32px;\n",
              "    padding: 0;\n",
              "    width: 32px;\n",
              "  }\n",
              "\n",
              "  .colab-df-quickchart:hover {\n",
              "    background-color: var(--hover-bg-color);\n",
              "    box-shadow: 0 1px 2px rgba(60, 64, 67, 0.3), 0 1px 3px 1px rgba(60, 64, 67, 0.15);\n",
              "    fill: var(--button-hover-fill-color);\n",
              "  }\n",
              "\n",
              "  .colab-df-quickchart-complete:disabled,\n",
              "  .colab-df-quickchart-complete:disabled:hover {\n",
              "    background-color: var(--disabled-bg-color);\n",
              "    fill: var(--disabled-fill-color);\n",
              "    box-shadow: none;\n",
              "  }\n",
              "\n",
              "  .colab-df-spinner {\n",
              "    border: 2px solid var(--fill-color);\n",
              "    border-color: transparent;\n",
              "    border-bottom-color: var(--fill-color);\n",
              "    animation:\n",
              "      spin 1s steps(1) infinite;\n",
              "  }\n",
              "\n",
              "  @keyframes spin {\n",
              "    0% {\n",
              "      border-color: transparent;\n",
              "      border-bottom-color: var(--fill-color);\n",
              "      border-left-color: var(--fill-color);\n",
              "    }\n",
              "    20% {\n",
              "      border-color: transparent;\n",
              "      border-left-color: var(--fill-color);\n",
              "      border-top-color: var(--fill-color);\n",
              "    }\n",
              "    30% {\n",
              "      border-color: transparent;\n",
              "      border-left-color: var(--fill-color);\n",
              "      border-top-color: var(--fill-color);\n",
              "      border-right-color: var(--fill-color);\n",
              "    }\n",
              "    40% {\n",
              "      border-color: transparent;\n",
              "      border-right-color: var(--fill-color);\n",
              "      border-top-color: var(--fill-color);\n",
              "    }\n",
              "    60% {\n",
              "      border-color: transparent;\n",
              "      border-right-color: var(--fill-color);\n",
              "    }\n",
              "    80% {\n",
              "      border-color: transparent;\n",
              "      border-right-color: var(--fill-color);\n",
              "      border-bottom-color: var(--fill-color);\n",
              "    }\n",
              "    90% {\n",
              "      border-color: transparent;\n",
              "      border-bottom-color: var(--fill-color);\n",
              "    }\n",
              "  }\n",
              "</style>\n",
              "\n",
              "  <script>\n",
              "    async function quickchart(key) {\n",
              "      const quickchartButtonEl =\n",
              "        document.querySelector('#' + key + ' button');\n",
              "      quickchartButtonEl.disabled = true;  // To prevent multiple clicks.\n",
              "      quickchartButtonEl.classList.add('colab-df-spinner');\n",
              "      try {\n",
              "        const charts = await google.colab.kernel.invokeFunction(\n",
              "            'suggestCharts', [key], {});\n",
              "      } catch (error) {\n",
              "        console.error('Error during call to suggestCharts:', error);\n",
              "      }\n",
              "      quickchartButtonEl.classList.remove('colab-df-spinner');\n",
              "      quickchartButtonEl.classList.add('colab-df-quickchart-complete');\n",
              "    }\n",
              "    (() => {\n",
              "      let quickchartButtonEl =\n",
              "        document.querySelector('#df-1d612e51-235b-467a-8fb4-d8488f7bf6cd button');\n",
              "      quickchartButtonEl.style.display =\n",
              "        google.colab.kernel.accessAllowed ? 'block' : 'none';\n",
              "    })();\n",
              "  </script>\n",
              "</div>\n",
              "    </div>\n",
              "  </div>\n"
            ]
          },
          "metadata": {},
          "execution_count": 12
        }
      ],
      "source": [
        "df = pd.read_csv('data/the weather of 187 countries in 2020.csv')\n",
        "df.head()"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 13,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "tGLI3Fhf3wxS",
        "outputId": "67c622e2-2427-4d1c-92a4-6a38647609cd"
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "Index(['STATION', 'Country/Region', 'DATE', 'Year', 'Month', 'Day', 'PRCP',\n",
              "       'SNWD', 'TAVG', 'TMAX', 'TMIN', 'SNOW', 'LATITUDE', 'LONGITUDE',\n",
              "       'ELEVATION', 'PRCP_ATTRIBUTES', 'TAVG_ATTRIBUTES', 'TMAX_ATTRIBUTES',\n",
              "       'TMIN_ATTRIBUTES', 'DAPR', 'MDPR', 'WESD', 'SNWD_ATTRIBUTES'],\n",
              "      dtype='object')"
            ]
          },
          "metadata": {},
          "execution_count": 13
        }
      ],
      "source": [
        "df.columns"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 14,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "vtBqcgRx3zMo",
        "outputId": "ae57b9dd-054e-4c8f-af0a-fe8d339a13cd"
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "(1392575, 23)"
            ]
          },
          "metadata": {},
          "execution_count": 14
        }
      ],
      "source": [
        "df.shape"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 15,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 320
        },
        "id": "DF-FS-OH316S",
        "outputId": "c7b7d820-e7b6-4252-f1ed-b2d450b93665"
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "            Year         Month           Day          PRCP           SNWD  \\\n",
              "count  1392575.0  1.392575e+06  1.392575e+06  1.043369e+06  377429.000000   \n",
              "mean      2020.0  4.279517e+00  1.595168e+01  2.564688e+00     120.712848   \n",
              "std          0.0  1.812637e+00  8.770296e+00  8.035237e+00     293.874318   \n",
              "min       2020.0  1.000000e+00  1.000000e+00  0.000000e+00     -20.000000   \n",
              "25%       2020.0  3.000000e+00  8.000000e+00  0.000000e+00       0.000000   \n",
              "50%       2020.0  4.000000e+00  1.600000e+01  0.000000e+00       0.000000   \n",
              "75%       2020.0  6.000000e+00  2.400000e+01  1.500000e+00      99.000000   \n",
              "max       2020.0  7.000000e+00  3.100000e+01  4.849000e+02   52900.000000   \n",
              "\n",
              "                TAVG           TMAX           TMIN           SNOW  \\\n",
              "count  878632.000000  866705.000000  898381.000000  105392.000000   \n",
              "mean       14.814992      17.412551       7.093554       3.742760   \n",
              "std        13.063075      12.707588      12.227766      19.093372   \n",
              "min       -56.200000     -55.000000     -65.000000       0.000000   \n",
              "25%         6.700000       8.400000       0.000000       0.000000   \n",
              "50%        16.800000      18.500000       7.700000       0.000000   \n",
              "75%        25.600000      27.222222      15.600000       0.000000   \n",
              "max        43.300000      51.200000      36.700000     625.000000   \n",
              "\n",
              "            LATITUDE      LONGITUDE      ELEVATION         DAPR       MDPR  \\\n",
              "count  104742.000000  104742.000000  104742.000000  1293.000000  81.000000   \n",
              "mean       37.689351      71.371220     787.542437     5.292343   0.958025   \n",
              "std        11.572761      71.760255    1094.757321     7.121322   1.653137   \n",
              "min       -17.817000    -140.850000       0.600000     1.000000   0.000000   \n",
              "25%        30.667000      75.983000      68.000000     2.000000   0.000000   \n",
              "50%        37.850000     104.500000     250.000000     3.000000   0.280000   \n",
              "75%        45.217000     116.117000    1099.000000     5.000000   1.510000   \n",
              "max        82.500000     131.983000    4701.000000    61.000000   9.240000   \n",
              "\n",
              "           WESD  \n",
              "count  2.000000  \n",
              "mean   0.050000  \n",
              "std    0.070711  \n",
              "min    0.000000  \n",
              "25%    0.025000  \n",
              "50%    0.050000  \n",
              "75%    0.075000  \n",
              "max    0.100000  "
            ],
            "text/html": [
              "\n",
              "  <div id=\"df-05ea2415-535a-49e0-96f0-5eff331eda61\" class=\"colab-df-container\">\n",
              "    <div>\n",
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
              "      <th>Year</th>\n",
              "      <th>Month</th>\n",
              "      <th>Day</th>\n",
              "      <th>PRCP</th>\n",
              "      <th>SNWD</th>\n",
              "      <th>TAVG</th>\n",
              "      <th>TMAX</th>\n",
              "      <th>TMIN</th>\n",
              "      <th>SNOW</th>\n",
              "      <th>LATITUDE</th>\n",
              "      <th>LONGITUDE</th>\n",
              "      <th>ELEVATION</th>\n",
              "      <th>DAPR</th>\n",
              "      <th>MDPR</th>\n",
              "      <th>WESD</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>count</th>\n",
              "      <td>1392575.0</td>\n",
              "      <td>1.392575e+06</td>\n",
              "      <td>1.392575e+06</td>\n",
              "      <td>1.043369e+06</td>\n",
              "      <td>377429.000000</td>\n",
              "      <td>878632.000000</td>\n",
              "      <td>866705.000000</td>\n",
              "      <td>898381.000000</td>\n",
              "      <td>105392.000000</td>\n",
              "      <td>104742.000000</td>\n",
              "      <td>104742.000000</td>\n",
              "      <td>104742.000000</td>\n",
              "      <td>1293.000000</td>\n",
              "      <td>81.000000</td>\n",
              "      <td>2.000000</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>mean</th>\n",
              "      <td>2020.0</td>\n",
              "      <td>4.279517e+00</td>\n",
              "      <td>1.595168e+01</td>\n",
              "      <td>2.564688e+00</td>\n",
              "      <td>120.712848</td>\n",
              "      <td>14.814992</td>\n",
              "      <td>17.412551</td>\n",
              "      <td>7.093554</td>\n",
              "      <td>3.742760</td>\n",
              "      <td>37.689351</td>\n",
              "      <td>71.371220</td>\n",
              "      <td>787.542437</td>\n",
              "      <td>5.292343</td>\n",
              "      <td>0.958025</td>\n",
              "      <td>0.050000</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>std</th>\n",
              "      <td>0.0</td>\n",
              "      <td>1.812637e+00</td>\n",
              "      <td>8.770296e+00</td>\n",
              "      <td>8.035237e+00</td>\n",
              "      <td>293.874318</td>\n",
              "      <td>13.063075</td>\n",
              "      <td>12.707588</td>\n",
              "      <td>12.227766</td>\n",
              "      <td>19.093372</td>\n",
              "      <td>11.572761</td>\n",
              "      <td>71.760255</td>\n",
              "      <td>1094.757321</td>\n",
              "      <td>7.121322</td>\n",
              "      <td>1.653137</td>\n",
              "      <td>0.070711</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>min</th>\n",
              "      <td>2020.0</td>\n",
              "      <td>1.000000e+00</td>\n",
              "      <td>1.000000e+00</td>\n",
              "      <td>0.000000e+00</td>\n",
              "      <td>-20.000000</td>\n",
              "      <td>-56.200000</td>\n",
              "      <td>-55.000000</td>\n",
              "      <td>-65.000000</td>\n",
              "      <td>0.000000</td>\n",
              "      <td>-17.817000</td>\n",
              "      <td>-140.850000</td>\n",
              "      <td>0.600000</td>\n",
              "      <td>1.000000</td>\n",
              "      <td>0.000000</td>\n",
              "      <td>0.000000</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>25%</th>\n",
              "      <td>2020.0</td>\n",
              "      <td>3.000000e+00</td>\n",
              "      <td>8.000000e+00</td>\n",
              "      <td>0.000000e+00</td>\n",
              "      <td>0.000000</td>\n",
              "      <td>6.700000</td>\n",
              "      <td>8.400000</td>\n",
              "      <td>0.000000</td>\n",
              "      <td>0.000000</td>\n",
              "      <td>30.667000</td>\n",
              "      <td>75.983000</td>\n",
              "      <td>68.000000</td>\n",
              "      <td>2.000000</td>\n",
              "      <td>0.000000</td>\n",
              "      <td>0.025000</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>50%</th>\n",
              "      <td>2020.0</td>\n",
              "      <td>4.000000e+00</td>\n",
              "      <td>1.600000e+01</td>\n",
              "      <td>0.000000e+00</td>\n",
              "      <td>0.000000</td>\n",
              "      <td>16.800000</td>\n",
              "      <td>18.500000</td>\n",
              "      <td>7.700000</td>\n",
              "      <td>0.000000</td>\n",
              "      <td>37.850000</td>\n",
              "      <td>104.500000</td>\n",
              "      <td>250.000000</td>\n",
              "      <td>3.000000</td>\n",
              "      <td>0.280000</td>\n",
              "      <td>0.050000</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>75%</th>\n",
              "      <td>2020.0</td>\n",
              "      <td>6.000000e+00</td>\n",
              "      <td>2.400000e+01</td>\n",
              "      <td>1.500000e+00</td>\n",
              "      <td>99.000000</td>\n",
              "      <td>25.600000</td>\n",
              "      <td>27.222222</td>\n",
              "      <td>15.600000</td>\n",
              "      <td>0.000000</td>\n",
              "      <td>45.217000</td>\n",
              "      <td>116.117000</td>\n",
              "      <td>1099.000000</td>\n",
              "      <td>5.000000</td>\n",
              "      <td>1.510000</td>\n",
              "      <td>0.075000</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>max</th>\n",
              "      <td>2020.0</td>\n",
              "      <td>7.000000e+00</td>\n",
              "      <td>3.100000e+01</td>\n",
              "      <td>4.849000e+02</td>\n",
              "      <td>52900.000000</td>\n",
              "      <td>43.300000</td>\n",
              "      <td>51.200000</td>\n",
              "      <td>36.700000</td>\n",
              "      <td>625.000000</td>\n",
              "      <td>82.500000</td>\n",
              "      <td>131.983000</td>\n",
              "      <td>4701.000000</td>\n",
              "      <td>61.000000</td>\n",
              "      <td>9.240000</td>\n",
              "      <td>0.100000</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div>\n",
              "    <div class=\"colab-df-buttons\">\n",
              "\n",
              "  <div class=\"colab-df-container\">\n",
              "    <button class=\"colab-df-convert\" onclick=\"convertToInteractive('df-05ea2415-535a-49e0-96f0-5eff331eda61')\"\n",
              "            title=\"Convert this dataframe to an interactive table.\"\n",
              "            style=\"display:none;\">\n",
              "\n",
              "  <svg xmlns=\"http://www.w3.org/2000/svg\" height=\"24px\" viewBox=\"0 -960 960 960\">\n",
              "    <path d=\"M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z\"/>\n",
              "  </svg>\n",
              "    </button>\n",
              "\n",
              "  <style>\n",
              "    .colab-df-container {\n",
              "      display:flex;\n",
              "      gap: 12px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert {\n",
              "      background-color: #E8F0FE;\n",
              "      border: none;\n",
              "      border-radius: 50%;\n",
              "      cursor: pointer;\n",
              "      display: none;\n",
              "      fill: #1967D2;\n",
              "      height: 32px;\n",
              "      padding: 0 0 0 0;\n",
              "      width: 32px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert:hover {\n",
              "      background-color: #E2EBFA;\n",
              "      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);\n",
              "      fill: #174EA6;\n",
              "    }\n",
              "\n",
              "    .colab-df-buttons div {\n",
              "      margin-bottom: 4px;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert {\n",
              "      background-color: #3B4455;\n",
              "      fill: #D2E3FC;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert:hover {\n",
              "      background-color: #434B5C;\n",
              "      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);\n",
              "      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));\n",
              "      fill: #FFFFFF;\n",
              "    }\n",
              "  </style>\n",
              "\n",
              "    <script>\n",
              "      const buttonEl =\n",
              "        document.querySelector('#df-05ea2415-535a-49e0-96f0-5eff331eda61 button.colab-df-convert');\n",
              "      buttonEl.style.display =\n",
              "        google.colab.kernel.accessAllowed ? 'block' : 'none';\n",
              "\n",
              "      async function convertToInteractive(key) {\n",
              "        const element = document.querySelector('#df-05ea2415-535a-49e0-96f0-5eff331eda61');\n",
              "        const dataTable =\n",
              "          await google.colab.kernel.invokeFunction('convertToInteractive',\n",
              "                                                    [key], {});\n",
              "        if (!dataTable) return;\n",
              "\n",
              "        const docLinkHtml = 'Like what you see? Visit the ' +\n",
              "          '<a target=\"_blank\" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'\n",
              "          + ' to learn more about interactive tables.';\n",
              "        element.innerHTML = '';\n",
              "        dataTable['output_type'] = 'display_data';\n",
              "        await google.colab.output.renderOutput(dataTable, element);\n",
              "        const docLink = document.createElement('div');\n",
              "        docLink.innerHTML = docLinkHtml;\n",
              "        element.appendChild(docLink);\n",
              "      }\n",
              "    </script>\n",
              "  </div>\n",
              "\n",
              "\n",
              "<div id=\"df-2f788137-999f-43f2-97da-c6b7a1c03502\">\n",
              "  <button class=\"colab-df-quickchart\" onclick=\"quickchart('df-2f788137-999f-43f2-97da-c6b7a1c03502')\"\n",
              "            title=\"Suggest charts.\"\n",
              "            style=\"display:none;\">\n",
              "\n",
              "<svg xmlns=\"http://www.w3.org/2000/svg\" height=\"24px\"viewBox=\"0 0 24 24\"\n",
              "     width=\"24px\">\n",
              "    <g>\n",
              "        <path d=\"M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zM9 17H7v-7h2v7zm4 0h-2V7h2v10zm4 0h-2v-4h2v4z\"/>\n",
              "    </g>\n",
              "</svg>\n",
              "  </button>\n",
              "\n",
              "<style>\n",
              "  .colab-df-quickchart {\n",
              "      --bg-color: #E8F0FE;\n",
              "      --fill-color: #1967D2;\n",
              "      --hover-bg-color: #E2EBFA;\n",
              "      --hover-fill-color: #174EA6;\n",
              "      --disabled-fill-color: #AAA;\n",
              "      --disabled-bg-color: #DDD;\n",
              "  }\n",
              "\n",
              "  [theme=dark] .colab-df-quickchart {\n",
              "      --bg-color: #3B4455;\n",
              "      --fill-color: #D2E3FC;\n",
              "      --hover-bg-color: #434B5C;\n",
              "      --hover-fill-color: #FFFFFF;\n",
              "      --disabled-bg-color: #3B4455;\n",
              "      --disabled-fill-color: #666;\n",
              "  }\n",
              "\n",
              "  .colab-df-quickchart {\n",
              "    background-color: var(--bg-color);\n",
              "    border: none;\n",
              "    border-radius: 50%;\n",
              "    cursor: pointer;\n",
              "    display: none;\n",
              "    fill: var(--fill-color);\n",
              "    height: 32px;\n",
              "    padding: 0;\n",
              "    width: 32px;\n",
              "  }\n",
              "\n",
              "  .colab-df-quickchart:hover {\n",
              "    background-color: var(--hover-bg-color);\n",
              "    box-shadow: 0 1px 2px rgba(60, 64, 67, 0.3), 0 1px 3px 1px rgba(60, 64, 67, 0.15);\n",
              "    fill: var(--button-hover-fill-color);\n",
              "  }\n",
              "\n",
              "  .colab-df-quickchart-complete:disabled,\n",
              "  .colab-df-quickchart-complete:disabled:hover {\n",
              "    background-color: var(--disabled-bg-color);\n",
              "    fill: var(--disabled-fill-color);\n",
              "    box-shadow: none;\n",
              "  }\n",
              "\n",
              "  .colab-df-spinner {\n",
              "    border: 2px solid var(--fill-color);\n",
              "    border-color: transparent;\n",
              "    border-bottom-color: var(--fill-color);\n",
              "    animation:\n",
              "      spin 1s steps(1) infinite;\n",
              "  }\n",
              "\n",
              "  @keyframes spin {\n",
              "    0% {\n",
              "      border-color: transparent;\n",
              "      border-bottom-color: var(--fill-color);\n",
              "      border-left-color: var(--fill-color);\n",
              "    }\n",
              "    20% {\n",
              "      border-color: transparent;\n",
              "      border-left-color: var(--fill-color);\n",
              "      border-top-color: var(--fill-color);\n",
              "    }\n",
              "    30% {\n",
              "      border-color: transparent;\n",
              "      border-left-color: var(--fill-color);\n",
              "      border-top-color: var(--fill-color);\n",
              "      border-right-color: var(--fill-color);\n",
              "    }\n",
              "    40% {\n",
              "      border-color: transparent;\n",
              "      border-right-color: var(--fill-color);\n",
              "      border-top-color: var(--fill-color);\n",
              "    }\n",
              "    60% {\n",
              "      border-color: transparent;\n",
              "      border-right-color: var(--fill-color);\n",
              "    }\n",
              "    80% {\n",
              "      border-color: transparent;\n",
              "      border-right-color: var(--fill-color);\n",
              "      border-bottom-color: var(--fill-color);\n",
              "    }\n",
              "    90% {\n",
              "      border-color: transparent;\n",
              "      border-bottom-color: var(--fill-color);\n",
              "    }\n",
              "  }\n",
              "</style>\n",
              "\n",
              "  <script>\n",
              "    async function quickchart(key) {\n",
              "      const quickchartButtonEl =\n",
              "        document.querySelector('#' + key + ' button');\n",
              "      quickchartButtonEl.disabled = true;  // To prevent multiple clicks.\n",
              "      quickchartButtonEl.classList.add('colab-df-spinner');\n",
              "      try {\n",
              "        const charts = await google.colab.kernel.invokeFunction(\n",
              "            'suggestCharts', [key], {});\n",
              "      } catch (error) {\n",
              "        console.error('Error during call to suggestCharts:', error);\n",
              "      }\n",
              "      quickchartButtonEl.classList.remove('colab-df-spinner');\n",
              "      quickchartButtonEl.classList.add('colab-df-quickchart-complete');\n",
              "    }\n",
              "    (() => {\n",
              "      let quickchartButtonEl =\n",
              "        document.querySelector('#df-2f788137-999f-43f2-97da-c6b7a1c03502 button');\n",
              "      quickchartButtonEl.style.display =\n",
              "        google.colab.kernel.accessAllowed ? 'block' : 'none';\n",
              "    })();\n",
              "  </script>\n",
              "</div>\n",
              "    </div>\n",
              "  </div>\n"
            ]
          },
          "metadata": {},
          "execution_count": 15
        }
      ],
      "source": [
        "df.describe()"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 16,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "zraoBQFT360h",
        "outputId": "c06fdd5d-0e62-413c-f786-9e342262ec46"
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "STATION            6911\n",
              "Country/Region      187\n",
              "DATE                188\n",
              "Year                  1\n",
              "Month                 7\n",
              "Day                  31\n",
              "PRCP               1353\n",
              "SNWD                779\n",
              "TAVG               1771\n",
              "TMAX               1075\n",
              "TMIN               1001\n",
              "SNOW                242\n",
              "LATITUDE           1219\n",
              "LONGITUDE          1473\n",
              "ELEVATION           992\n",
              "PRCP_ATTRIBUTES       3\n",
              "TAVG_ATTRIBUTES       1\n",
              "TMAX_ATTRIBUTES       3\n",
              "TMIN_ATTRIBUTES       3\n",
              "DAPR                 46\n",
              "MDPR                 48\n",
              "WESD                  2\n",
              "SNWD_ATTRIBUTES       4\n",
              "dtype: int64"
            ]
          },
          "metadata": {},
          "execution_count": 16
        }
      ],
      "source": [
        "df.nunique()"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 17,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "lcvKqwBQ37ih",
        "outputId": "86ee6297-40fa-4eae-9d26-f9146ff361e0"
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "array(['Comoros', 'Georgia', 'Nepal', 'Philippines', 'Monaco', 'US',\n",
              "       'Australia', 'Namibia', 'Saint Lucia', 'Lebanon', 'Zambia',\n",
              "       'Malaysia', 'Peru', 'Kenya', 'Belarus', 'Iceland', 'Lesotho',\n",
              "       'Venezuela', 'Albania', 'Tanzania', 'Greece', 'Barbados',\n",
              "       'Singapore', 'Switzerland', 'Sri Lanka', 'China', 'Gabon',\n",
              "       'Guinea-Bissau', 'Congo (Brazzaville)', 'United Arab Emirates',\n",
              "       'Tajikistan', 'Syria', 'Lithuania', 'Paraguay', 'Romania',\n",
              "       'Maldives', 'Jamaica', 'Kuwait', 'Finland', 'Argentina',\n",
              "       'Ethiopia', 'Japan', 'Cameroon', 'Bhutan', 'Botswana', 'Pakistan',\n",
              "       'Brazil', 'Madagascar', 'Eritrea', 'Liberia', 'Mali', 'Thailand',\n",
              "       'Egypt', 'Ireland', 'Belgium', 'Luxembourg', 'Fiji', 'Italy',\n",
              "       'Greenland', 'Antigua and Barbuda',\n",
              "       'Saint Vincent and the Grenadines', 'Andorra', 'Guinea', 'Nigeria',\n",
              "       'Ecuador', 'Guatemala', 'Afghanistan', 'Suriname', 'Djibouti',\n",
              "       'Uganda', 'Niger', 'Israel', 'Russia', 'Chile', 'Mexico',\n",
              "       'Seychelles', 'Bosnia and Herzegovina', 'Montenegro',\n",
              "       'Trinidad and Tobago', 'Togo', 'Panama', 'Denmark', 'Malta',\n",
              "       'Sierra Leone', 'Bahamas', 'Taiwan', 'Kyrgyzstan', 'South Africa',\n",
              "       'Sao Tome and Principe', 'New Zealand', 'France', 'Qatar',\n",
              "       'Angola', 'Belize', 'Azerbaijan', 'San Marino', 'Saudi Arabia',\n",
              "       'Serbia', 'Turkey', 'Cuba', 'Nicaragua', 'Uruguay', 'Jordan',\n",
              "       'Timor-Leste', 'Grenada', 'Slovenia', 'Portugal', 'Western Sahara',\n",
              "       'Costa Rica', 'Mauritius', 'Dominica', 'Bolivia', 'Cambodia',\n",
              "       'Austria', 'Poland', 'Czechia', 'India', 'Somalia', 'Algeria',\n",
              "       'Brunei', 'Latvia', 'Gambia', 'Uzbekistan', 'Armenia', 'Slovakia',\n",
              "       'North Macedonia', 'Guyana', 'Cyprus', 'United Kingdom',\n",
              "       \"Cote d'Ivoire\", 'Honduras', 'Mozambique', 'Oman', 'Iran',\n",
              "       'Mongolia', 'Hungary', 'West Bank and Gaza', 'Bahrain', 'Chad',\n",
              "       'Kazakhstan', 'Holy See', 'Congo (Kinshasa)', 'Burkina Faso',\n",
              "       'Dominican Republic', 'Ghana', 'Zimbabwe', 'Sudan', 'Benin',\n",
              "       'Estonia', 'Haiti', 'Indonesia', 'Saint Kitts and Nevis',\n",
              "       'Netherlands', 'Croatia', 'Canada', 'Yemen', 'Eswatini', 'Moldova',\n",
              "       'Norway', 'Equatorial Guinea', 'Ukraine', 'Tunisia', 'South Korea',\n",
              "       'Burma', 'Senegal', 'Vietnam', 'Kosovo', 'Liechtenstein', 'Malawi',\n",
              "       'Central African Republic', 'South Sudan', 'Iraq', 'Morocco',\n",
              "       'Papua New Guinea', 'Cabo Verde', 'Mauritania', 'Sweden',\n",
              "       'Germany', 'Laos', 'El Salvador', 'Rwanda', 'Bangladesh', 'Libya',\n",
              "       'Burundi', 'Bulgaria', 'Spain', 'Colombia'], dtype=object)"
            ]
          },
          "metadata": {},
          "execution_count": 17
        }
      ],
      "source": [
        "df['Country/Region'].unique()"
      ]
    },
    {
      "cell_type": "markdown",
      "source": [
        "CHECKING FOR NUMBER OF NULL VALUES IN ALL THE ATTRIBUTES"
      ],
      "metadata": {
        "id": "48vQLBFDtp8K"
      }
    },
    {
      "cell_type": "code",
      "execution_count": 18,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "eJniWSRk2Wzo",
        "outputId": "a2dc2b48-3d3e-41ee-933c-c92712ab9383"
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "STATION                  0\n",
              "Country/Region           0\n",
              "DATE                     0\n",
              "Year                     0\n",
              "Month                    0\n",
              "Day                      0\n",
              "PRCP                349206\n",
              "SNWD               1015146\n",
              "TAVG                513943\n",
              "TMAX                525870\n",
              "TMIN                494194\n",
              "SNOW               1287183\n",
              "LATITUDE           1287833\n",
              "LONGITUDE          1287833\n",
              "ELEVATION          1287833\n",
              "PRCP_ATTRIBUTES    1386568\n",
              "TAVG_ATTRIBUTES    1388725\n",
              "TMAX_ATTRIBUTES    1386938\n",
              "TMIN_ATTRIBUTES    1386701\n",
              "DAPR               1391282\n",
              "MDPR               1392494\n",
              "WESD               1392573\n",
              "SNWD_ATTRIBUTES    1392221\n",
              "dtype: int64"
            ]
          },
          "metadata": {},
          "execution_count": 18
        }
      ],
      "source": [
        "df.isnull().sum()"
      ]
    },
    {
      "cell_type": "markdown",
      "source": [
        "SINCE MANY COLUMNS HAVE NULL VALUES IN LARGE NUMBERS AND IF WE FILL IT, IT WILL AFFECT OUR MODEL. HENCE,DROPPING THOSE COLUMNS."
      ],
      "metadata": {
        "id": "xxHGQjDUt0GH"
      }
    },
    {
      "cell_type": "code",
      "execution_count": 19,
      "metadata": {
        "id": "tco_ozVd3BqH"
      },
      "outputs": [],
      "source": [
        "country = df['Country/Region'].unique()\n",
        "weather_df = df.drop(['Year','PRCP_ATTRIBUTES', 'TAVG_ATTRIBUTES', 'TMAX_ATTRIBUTES',\n",
        "                        'TMIN_ATTRIBUTES', 'DAPR', 'MDPR', 'WESD', 'SNWD_ATTRIBUTES',\n",
        "                        'SNOW','LATITUDE','LONGITUDE','SNWD','ELEVATION'], axis=1)"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 20,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "HGulQsR9skKH",
        "outputId": "23c41fba-183c-47f4-d6d3-7f4a12ad8c72"
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "Index(['STATION', 'Country/Region', 'DATE', 'Month', 'Day', 'PRCP', 'TAVG',\n",
              "       'TMAX', 'TMIN'],\n",
              "      dtype='object')"
            ]
          },
          "metadata": {},
          "execution_count": 20
        }
      ],
      "source": [
        "weather_df.columns"
      ]
    },
    {
      "cell_type": "markdown",
      "source": [
        "FINDING CORRELATION OF THE FEATURES"
      ],
      "metadata": {
        "id": "18yLfc4J1hJo"
      }
    },
    {
      "cell_type": "code",
      "execution_count": 21,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 861
        },
        "id": "i1i5sxru5B2u",
        "outputId": "75b3695c-e86c-4fdf-dc3b-7426906985a9"
      },
      "outputs": [
        {
          "output_type": "stream",
          "name": "stderr",
          "text": [
            "<ipython-input-21-ec0f84accebf>:2: FutureWarning: The default value of numeric_only in DataFrame.corr is deprecated. In a future version, it will default to False. Select only valid columns or specify the value of numeric_only to silence this warning.\n",
            "  sns.heatmap(weather_df.corr(), annot=True);\n"
          ]
        },
        {
          "output_type": "display_data",
          "data": {
            "text/plain": [
              "<Figure size 800x800 with 2 Axes>"
            ],
            "image/png": "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dSIiIiIiDcRAnYiIiIhIAzH1hYiIiIjUind9KRvOqBMRERERaSAG6kREREREGoipL0RERESkVgJTX8qEM+pERERERBqIgToRERERkQZi6gsRERERqRW/8KhsOKNORERERKSBGKgTEREREWkgpr4QERERkVrxri9lwxl1IiIiIiINxBl1IiIiIlIrzqiXDWfUiYiIiIg0EAN1IiIiIiINxNQXIiIiIlIrJr6UDWfUiYiIiIg0EAN1IiIiIiINJBG4DLdc5OfnY/HixQgKCoKenl5FN6fa43hoDo6FZuF4aA6OhWbheJAmYqBeTjIzM2FqaoqMjAyYmJhUdHOqPY6H5uBYaBaOh+bgWGgWjgdpIqa+EBERERFpIAbqREREREQaiIE6EREREZEGYqBeTvT09DB79mwuQNEQHA/NwbHQLBwPzcGx0CwcD9JEXExKRERERKSBOKNORERERKSBGKgTEREREWkgBupERERERBqIgToRERERkQZioK4BJBIJduzYUdHNICIiIiINUq0DdX9/f0gkEowePbrEtrFjx0IikcDf37/czjdnzhw0b9683I5X3TwZL4lEAh0dHdjY2KBz584ICwuDQqGo6OZVac++9rq6unBycsK8efNQWFiIgwcPitskEgmsrKzw8ccf4+zZs0rHKCgowNKlS+Hu7g4DAwNYWlqiXbt2kMlkkMvlrzwPQel1VvWYM2eOWNfFxQV6enq4c+eOWNajRw907dpV5bEPHz4MiUSCM2fOiGWxsbHo0KEDzM3Noa+vj0aNGiEgIACnTp1SWx8rg9KMw40bNyCRSKCtrY1///1Xaf/U1FRIpVJIJBLcuHGjxPG9vLygra2NY8eOKZUXFRXBw8MDffv2VSrPyMiAg4MDZs6cWe59rUzUMS5P6icmJio9t7a2RlZWltL+zZs3V/obJCoP1TpQBwAHBwdER0cjNzdXLMvLy0NUVBTq1KlTgS0jVbp27YrU1FTcuHEDe/bsgaenJyZOnIju3bszmFOzJ699UlISJk+ejDlz5mDZsmXi9suXLyM1NRX79u1Dfn4+vL29UVBQAKA4SPfy8kJwcDBGjhyJhIQEHD16FGPHjsXq1atx/vz5Up+nOktNTRUfK1euhImJiVLZlClTAABHjhxBbm4u+vfvj4iICHH/wMBA/P7777h161aJY8tkMrRs2RLNmjUDAEyf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\n"
          },
          "metadata": {}
        }
      ],
      "source": [
        "plt.figure(figsize=(8,8))\n",
        "sns.heatmap(weather_df.corr(), annot=True);\n",
        "plt.tight_layout()"
      ]
    },
    {
      "cell_type": "markdown",
      "source": [
        "FILLING THE NULLS VALUES USING MODE"
      ],
      "metadata": {
        "id": "1NjRO0Ee1oyp"
      }
    },
    {
      "cell_type": "code",
      "execution_count": 22,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "d6Vuwleo59_B",
        "outputId": "7e3082ec-5215-4d6d-ed3b-4d26234c6492"
      },
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "1305\n",
            "1305\n",
            "1305\n",
            "1305\n"
          ]
        }
      ],
      "source": [
        "import statistics  # Import the statistics module to calculate the mode\n",
        "weather_df_copy = weather_df.copy()\n",
        "from sklearn.preprocessing import LabelEncoder\n",
        "\n",
        "weather_df_copy = weather_df.copy()\n",
        "\n",
        "countries = weather_df_copy['Country/Region']\n",
        "label_encoder = LabelEncoder()\n",
        "encoded_countries = label_encoder.fit_transform(countries)\n",
        "weather_df_copy['Country/Region'] = encoded_countries\n",
        "def calculate_mode(data):\n",
        "    # Convert the data to a list of integers and filter out None values\n",
        "    data_as_int = [int(value) for value in data if not math.isnan(value)]\n",
        "\n",
        "    try:\n",
        "        mode_value = statistics.mode(data_as_int)\n",
        "        return mode_value\n",
        "    except statistics.StatisticsError:\n",
        "        return None  # Return None if there is no unique mode\n",
        "\n",
        "average_temp = weather_df_copy.groupby(['Country/Region', 'Month'])['TAVG'].apply(calculate_mode).to_dict()\n",
        "average_temp_min = weather_df_copy.groupby(['Country/Region', 'Month'])['TMIN'].apply(calculate_mode).to_dict()\n",
        "average_temp_max = weather_df_copy.groupby(['Country/Region', 'Month'])['TMAX'].apply(calculate_mode).to_dict()\n",
        "average_prcp = weather_df_copy.groupby(['Country/Region', 'Month'])['PRCP'].apply(calculate_mode).to_dict()\n",
        "print(len(average_temp_min))\n",
        "print(len(average_temp_max))\n",
        "print(len(average_temp))\n",
        "print(len(average_prcp))\n"
      ]
    },
    {
      "cell_type": "markdown",
      "source": [
        "LABEL ENCODING COUNTRY COLUMN"
      ],
      "metadata": {
        "id": "Ajurjdyn1616"
      }
    },
    {
      "cell_type": "code",
      "execution_count": 23,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "fLaFlhbfpu8m",
        "outputId": "554ea580-e21f-480c-eae9-b56a2378adfb"
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "STATION           0\n",
              "Country/Region    0\n",
              "DATE              0\n",
              "Month             0\n",
              "Day               0\n",
              "PRCP              0\n",
              "TAVG              0\n",
              "TMAX              0\n",
              "TMIN              0\n",
              "dtype: int64"
            ]
          },
          "metadata": {},
          "execution_count": 23
        }
      ],
      "source": [
        "def fill_missing_avg_temp(row,temp_type):\n",
        "    key = (row['Country/Region'], row['Month'])\n",
        "    if(temp_type == 'TAVG'):\n",
        "      return average_temp.get(key, row[temp_type])\n",
        "    elif(temp_type == 'TMIN'):\n",
        "      return average_temp_min.get(key, row[temp_type])\n",
        "    elif(temp_type == 'PRCP'):\n",
        "      return average_prcp.get(key, row[temp_type])\n",
        "    else:\n",
        "      return average_temp_max.get(key, row[temp_type])\n",
        "\n",
        "weather_df_copy['TAVG'] = weather_df_copy.apply(fill_missing_avg_temp, args=['TAVG'] ,axis = 1)\n",
        "weather_df_copy['TMIN'] = weather_df_copy.apply(fill_missing_avg_temp, args=['TMIN'] ,axis = 1)\n",
        "weather_df_copy['TMAX'] = weather_df_copy.apply(fill_missing_avg_temp, args=['TMAX'] ,axis = 1)\n",
        "weather_df_copy['PRCP'] = weather_df_copy.apply(fill_missing_avg_temp, args=['PRCP'] ,axis = 1)\n",
        "weather_df_copy.fillna(method='ffill', inplace=True)\n",
        "weather_df_copy.isnull().sum()"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 24,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "J0485-xsvf95",
        "outputId": "9386a389-f333-4f8e-ca3e-f2c421413dc9"
      },
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "<class 'pandas.core.frame.DataFrame'>\n",
            "Int64Index: 1392575 entries, 0 to 1392574\n",
            "Data columns (total 9 columns):\n",
            " #   Column          Non-Null Count    Dtype  \n",
            "---  ------          --------------    -----  \n",
            " 0   STATION         1392575 non-null  object \n",
            " 1   Country/Region  1392575 non-null  int64  \n",
            " 2   DATE            1392575 non-null  object \n",
            " 3   Month           1392575 non-null  int64  \n",
            " 4   Day             1392575 non-null  int64  \n",
            " 5   PRCP            1392575 non-null  float64\n",
            " 6   TAVG            1392575 non-null  int64  \n",
            " 7   TMAX            1392575 non-null  float64\n",
            " 8   TMIN            1392575 non-null  float64\n",
            "dtypes: float64(3), int64(4), object(2)\n",
            "memory usage: 106.2+ MB\n"
          ]
        }
      ],
      "source": [
        "weather_df_copy.isnull().sum()\n",
        "weather_df_copy = weather_df_copy.dropna(subset=['TMIN','TMAX','PRCP'])\n",
        "weather_df_copy.info()"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 25,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 860
        },
        "id": "rRNPQQCeXJE3",
        "outputId": "fde487cc-7b03-44d0-fe4a-a01ccd1ac27a"
      },
      "outputs": [
        {
          "output_type": "stream",
          "name": "stderr",
          "text": [
            "<ipython-input-25-28a7a1a20e44>:2: FutureWarning: The default value of numeric_only in DataFrame.corr is deprecated. In a future version, it will default to False. Select only valid columns or specify the value of numeric_only to silence this warning.\n",
            "  sns.heatmap(weather_df_copy.corr(), annot=True);\n"
          ]
        },
        {
          "output_type": "display_data",
          "data": {
            "text/plain": [
              "<Figure size 800x800 with 2 Axes>"
            ],
            "image/png": "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lSsyB0REREREJYyImfK8yNQp/zSe/JOMjAw8fvwYPj4+sLe3L4y4iIiIiIh+GjJ1ylevXi21fN68eXj79u13BURERERE9LMp1DHlAwcOxM6dOwvzkERERERU3AmFit2KgULtlN+9excaGhqFeUgiIiIiohJPpuErf/75p8RnkUiEN2/ewMPDA7Nnzy6UwIiIiIiohOBEzzzJ1CnX09OT+KykpIQqVapgwYIFaNu2baEERkRERET0s5CpU75r167CjoOIiIiI6KclU6f8E09PT/j7+wMAqlevjjp16hRKUERERERUghSTyZaKJFOnPDo6Gn379sW1a9egr68PAEhMTESrVq1w4MABmJiYFGaMREREREQlmkyrr4wbNw4pKSnw9fVFfHw84uPj4ePjg+TkZIwfP76wYyQiIiKi4kwkVOxWDMiUKT937hwuXbqEatWqictsbW2xceNGTvQkIiIiIiogmTLlQqEQqqqqOcpVVVUh5JghIiIiIqICkalT3rp1a0yYMAGvX78Wl0VERGDSpEn47bffCi04IiIiIioB+EbPPMnUKd+wYQOSk5NhZWUFGxsb2NjYoEKFCkhOTsb69esLO0YiIiIiohJNpjHllpaW8PLywqVLl/Ds2TMAQLVq1dCmTZtCDY6IiIiISoBikq1WpAJlyq9cuQJbW1skJydDIBDg999/x7hx4zBu3Dg0aNAA1atXx82bN+UVKxERERFRiVSgTPmaNWswbNgw6Orq5tinp6eHESNGYNWqVWjevHmBA6lTvX+B29C3PfLdr+gQShzNMgV/tilv9Y0rKTqEEmd3KS1Fh1Di6Bh9UHQIJc7rcD1Fh0BUZBQoU/7kyRP88ccfue5v27YtPD09vzsoIiIiIipBuE55ngrUKY+KipK6FOInKioqiImJ+e6giIiIiIh+JgUavmJhYQEfHx9UrFhR6n5vb2+ULl26UAIjIiIiohKCEz3zVKBMeYcOHTB79mx8+JBzXF1qairmzp2LTp06FVpwREREREQ/gwJlyl1dXXHs2DFUrlwZY8eORZUqVQAAz549w8aNG5GVlYVZs2bJJVAiIiIiopKqQJ1yMzMz3LlzB6NGjcKMGTMgEokAAAKBAO3atcPGjRthZmYml0CJiIiIqJgqJpMtFanALw8qX748zpw5g4SEBAQHB0MkEqFSpUowMDCQR3xERERERCWe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lwcRERERERWEiG/0zFOBJ3oSEREREVHhYqeciIiIiEjBvmudciIiIiKiPHGiZ56YKSciIiIiUjB2yomIiIiIFIzDV4iIiIhIvkRcfSUvzJQTERERESkYM+VEREREJF+c6JknZsqJiIiIiBSMnXIiIiIiIgXj8BUiIiIiki8hJ3rmhZlyIiIiIiIFY6aciIiIiOSLEz3zxEw5EREREZGCsVNORERERKRgHL5CRERERPLFN3rmiZlyIiIiIiIFY6aciIiIiOSLEz3zxEw5EREREZGCsVNORERERKRgHL5CRERERHIl4hs988RMORERERGRghWZTLmaUpEJpcTQLNNc0SGUOKmvbyo6hBKpYc3Big6hxGkfF6HoEEqcrFhm+gqbsiBO0SGUSKGKDkAaTvTMEzPlREREREQKxk45EREREZGCccwIEREREckXh6/kiZlyIiIiIiIFY6aciIiIiORLxInSeWGmnIiIiIhIwdgpJyIiIiJSMA5fISIiIiL54kTPPDFTTkRERESkYMyUExEREZFciZgpzxMz5URERERECsZOORERERGRgnH4ChERERHJF4ev5ImZciIiIiIiBWOmnIiIiIjkS8g3euaFmXIiIiIiIgVjp5yIiIiISME4fIWIiIiI5IsTPfPETDkRERERkYIxU05ERERE8sVMeZ6YKSciIiIiUjB2yomIiIiIFIzDV4iIiIhIrkQiDl/JCzPlREREREQKxkw5EREREckXJ3rmiZlyIiIiIiIFY6eciIiIiEjBOHyFiIiIiOSLw1fyxEw5EREREZGCMVNORERERHIlYqY8T8yUExEREREpGDvlREREREQKxuErRERERCRfHL6SJ2bKiYiIiIgUTKZM+bt376CtrV3YsRARERFRSSRUdABFn0yZcjMzMzg6OuLWrVuFHQ8RERERkcJt3LgRVlZW0NDQQMOGDfHgwYNv1k9MTMSYMWNQunRpqKuro3Llyjhz5ky+zydTp/zff/9FfHw8WrdujcqVK2PZsmV4/fq1LIciIiIiIipSDh48CGdnZ8ydOxdeXl6oVasW2rVrh+joaKn109PT8fvvvyMsLAxHjhxBQEAAtm3bBgsLi3yfU6ZOebdu3XD8+HFERERg5MiR2L9/P8qXL49OnTrh2LFjyMzMlOWwRERERFQCiYQihW4FtWrVKgwbNgwODg6wtbXF5s2b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3t4+zzpceYWIiIiIvlRcJlsqUoE65bt27ZJXHEREREREP60CTfQkIiIiIqLCV6BMORERERFRgXH4Sp6YKSciIiIiUjBmyomIiIhIrjjRM2/MlBMRERERKRg75URERERECsbhK0REREQkVxy+kjdmyomIiIiIFIyZciIiIiKSK2bK88ZMORERERGRgrFTTkRERESkYBy+QkRERETyJRIoOoIij5lyIiIiIiIFY6aciIiIiOSKEz3zxkw5EREREZGCsVNORERERKRgHL5CRERERHIlEnKiZ16YKSciIiIiUjB2yomIiIiIFIzDV4iIiIhIrrj6St6YKSciIiIiUjBmyomIiIhIrkR8o2eemCknIiIiIlIwdsqJiIiIiBSMw1eIiIiISK440TNvzJQTERERESkYM+VEREREJFd8o2femCknIiIiIlIwdsqJiIiIiBSMw1eIiIiISK5EIkVHUPQVmU65oYq2okMoceobV1J0CCVOw5qDFR1CiXT/6R5Fh1Di9K83SdEhlDhZYK+isKnzC3sisSLTKSciIiKikokTPfPGX1GJiIiIiBSMnXIiIiIiIgXj8BUiIiIikisOX8kbM+VERERERArGTDkRERERyRWXRMwbM+VERERERArGTjkRERERkYJx+AoRERERyRUneuaNmXIiIiIiIgVjppyIiIiI5EokYqY8L8yUExEREREpGDvlREREREQKxuErRERERCRXIqGiIyj6mCknIiIiIlIwZsqJiIiISK6EnOiZJ2bKiYiIiIgUjJ1yIiIiIiIF4/AVIiIiIpIrrlOeN2bKiYiIiIgUjJlyIiIiIpIrkZCZ8rwwU05EREREpGDslBMRERERKRiHrxARERGRXIlEio6g6GOmnIiIiIhIwZgpJyIiIiK54kTPvDFTTkRERESkYOyUExEREREpGIevEBEREZFcCflGzzwxU05EREREpGDMlBMRERGRXImYKc9TgTLlQqEQy5cvR9OmTdGgQQNMnz4dqamp8oqNiIiIiOinUKBO+eLFizFz5kyUKlUKFhYWWLt2LcaMGSOv2IiIiIiIfgoF6pTv2bMHf//9N86fP4/jx4/j1KlT2LdvH4RCobziIyIiIqJiTiRS7FYcFKhTHh4ejg4dOog/t2nTBgKBAK9fvy70wIiIiIiIfhYFmuiZmZkJDQ0NiTJVVVVkZGQUalBERERE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vH79GmXLlpU5CCIiIiIquURQ7JKIM2bMgLOzs0SZurp6oRw7JSUFgwYNwrZt22BsbCzzcQrUKc/MzISGhoZEmaqqKjIyMmQOgIiIiIhIntTV1fPdCTc2NoaysjKioqIkyqOiomBubp6jfkhICMLCwtC5c2dx2adRJCoqKggICICNjU2e5y1Qp1wkEmHIkCESF/XhwweMHDkS2tra4rJjx44V5LBEREREREWCmpoa6tWrh8uXL4uXNRQKhbh8+TLGjh2bo37VqlXx9OlTiTJXV1ekpKRg7dq1sLS0zNd5C9Qpt7e3z1E2cODAghyCiIiIiH4yQpGiIygYZ2dn2Nvbo379+vjll1+wZs0avHv3Trway+DBg2FhYYGlS5dCQ0MDNWrUkGivr68PADnKv6VAnfJdu3YVpDoRERERUbHTp08fxMTEYM6cOYiMjETt2rVx7tw58eTP8PBwKCkVaL2UPBWoU05EREREVFBCBU/0lMXYsWOlDlcBgGvXrn2z7e7duwt8vsLt4hMRERERUYGxU05EREREpGAcvkJEREREcqXodcqLA2bKiYiIiIgUjJlyIiIiIpIroaIDKAaYKSciIiIiUjB2yomIiIiIFIzDV4iIiIhIrjjRM2/MlBMRERERKRgz5UREREQkV5zomTdmyomIiIiIFIydciIiIiIiBePwFSIiIiKSKw5fyRsz5URERERECsZMORERERHJFZdEzBsz5URERERECsZOORERERGRgnH4ChERERHJlZCjV/LETDkRERERkYIxU05EREREciXkRM88MVNORERERKRg7JQTERERESkYh68QERERkVyJFB1AMcBMORERERGRgrFTTkRERESkYEVm+EqqMEPRIZQ4u0tpKTqEEqd9XISiQyiR+tebpOgQSpz9nqsVHUKJI0qOVXQIJY7obYKiQ6AfRKjoAIoBZsqJiIiIiBSsyGTKiYiIiKhkEgq4TnlemCknIiIiIlIwdsqJiIiIiBSMw1eIiIiISK64TnnemCknIiIiIlIwZsqJiIiISK64JGLemCknIiIiIlIwdsqJiIiIiBSMw1eIiIiISK6EXKY8T8yUExEREREpGDPlRERERCRXQjBVnhdmyomIiIiIFIydciIiIiIiBePwFSIiIiKSK77RM2/MlBMRERERKRgz5UREREQkV1wSMW/MlBMRERERKRg75URE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WLx4MU6ePAkPD48CxchKORERERFplNhLIhoZGcHc3FzhkV9SbmhoiNq1aytM0vx30mbDhg3zPcelS5di/vz5OHr0KOrUqVPga8RKORERERHROyZOnIghQ4agTp06qFevHlatWoUXL17A09MTADB48GCULl1a3gKzZMkSzJ49Gzt27EC5cuUQGxsLADA1NYWpqala78mknIiIiIjoHX369EFCQgJmz56N2NhY1KhRA0ePHpVP/oyKioJU+rbh5JdffkFWVhZ69eql8Dpz5szBd999p9Z7MiknIiIiIo36mLXCxTZmzBiMGTNG6b4zZ84oPH/48OF/fj/2lBMRERERiYyVciIiIiLSKBkEsUP45LFSTkREREQkMiblREREREQiY/sKEREREWkUm1dUY6WciIiIiEhkn0ylXAqJ2CHoHLMSr8QOQefkJmrjok6fvlzWUAqd8CxR7BB0jsTcRuwQdI4s+o7YIVAR4V9P1VgpJyIiIiISGZNyIiIiIiKRfTLtK0RERESkmwS2KarESjkRERERkciYlBMRERERiYztK0RERESkUVx9RTVWyomIiIiIRMZKORERERFplIwTPVVipZyIiIiISGRMyomIiIiIRMb2FSIiIiLSKDavqMZKORERERGRyFgpJyIiIiKN4kRP1VgpJyIiIiISGZNyIiIiIiKRsX2FiIiIiDSKd/RUjZVyIiIiIiKRsVJORERERBolcKKnSqyUExERERGJjEk5EREREZHI2L5CRERERBrFiZ6qsVJORERERCQyVsqJiIiISKM40VM1VsqJiIiIiETGpJyIiIiISGRsXyEiIiIijeJET9VYKSciIiIiEpnaSfmsWbOQk5OT7/6oqCi0adOmUIIiIiIiIt0hEwRRH9pA7aR8y5YtqFu3LkJCQvLsW79+PapWrQp9fXbDEBEREREVlNpJeUhICKpVq4Y6depg0aJFkMlkiIqKQuvWrfHNN99g2bJlOHLkiCZjJSIiIiLSSWqXts3NzbF161b07NkTI0eOxK5duxAZGYl69eohODgYZcuW1WScRERERKSltKOBRFwFnujZoEEDVKtWDcHBwZDJZJg5cyYTciIiIiKi/6BASXlAQADc3d0hk8kQFhYGHx8ftG3bFhMmTMCrV680FSMRERERaTEZBFEf2kDtpLxnz54YPnw4vvvuO5w6dQpubm5YunQp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SgtbwzsJYoegk+qYOaseRAWy86+ZYoegcyTm6rVokvpyw86LHYJOMm46SOwQ8vjSqYuo778/6pCo768Otb9bcXBwwNSpUxEeHo69e/ciJSUF9evXR4MGDbBx40bIZGzhJyIiIqK8ZBBEfWiDj2p4atKkCTZv3ox79+6hWLFiGDVqFFJTUws5NCIiIiKiz8NHJeUXLlzAsGHDULFiRaSnp2Pt2rWwtLQs5NCIiIiISBfIRH5oA7Vna8bExGDr1q3w8/NDSkoKBgwYgPPnz6Nq1aqajI+IiIiISOepnZQ7OTmhdOnSGDJkCLp27QoDAwPIZDIEBwcrjPPw8MjnFYiIiIiISBm1k/Lc3FxERUVh/vz5WLBgAYC8a06qu045EREREX0+3r/JEuWldlIeGRmpehARERERERWY2kn5li1bMHnyZBQrVkyT8RARERGRjtGWZQnFpPbqK3PnzkV6eromYyEiIiIi+iypnZSreeNPIiIiIiIqILXbV4DXEzmJiIiIiAqCxV3VCpSUV6xYUWVinpyc/J8CIiIiIiL63BQoKZ87dy4sLCw0FQsRERER6SBtuaummAqUlPft2xd2dnaaioWIiIiI6LOk9kRP9pMTEREREWmG2pVyNugTERER0cfgHT1VUzspl8nYDUREREREpAkF6iknIiIiIioo3tFTNbV7yomIiIiISDOYlBMRERERiYztK0RERESkUVwwRDVWyomIiIiIRMZKORERERFpFCd6qsZKORERERGRyJiUExERERGJjO0rRERERKRRvKOnaqyUExERERGJjJVyIiIiItIoGZdEVImVciIiIiIikTEpJyIiIiISGdtXiIiIiEij2LyiGivlREREREQiY6WciIiIiDSKd/RUjZVyIiIiIiKRMSknIiIiIhIZ21eIiIiISKPYvqIaK+VERERERCJjpZyIiIiINErgHT1VYqWciIiIiEhkTMqJiIiIiETG9hUiIiIi0ihO9FSNSbkOexplIXYIOkdPkiR2CDrJiF/aFTohPUXsEHSOLPqO2CHoHL3KjcUOgeiTwaSciIiIiDRKYKVcJZaniIiIiIhExqSciIiIiOg9a9euRbly5WBsbIz69evjypUrHxy/Z88eVKpUCcbGxqhWrRoOHz5coPdjUk5EREREGiUIgqiPgtq1axcmTpyIOXPmICgoCNWrV0e7du0QHx+v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0hVcfUWFbt26QSKRiB0GEREREekwVsqJiIiIiETGnnIVypcvj6SkpDzbU1NTUb58eREiIiIiIiJdw6RchYcPHypdfSUzMxNPnjwRISIiIiIi0jXsKc/HwYMH5f9/7NgxWFhYyJ/n5ubi1KlTcHZ2FiM0IiIiItIx7CnPh1T6+ksEiUSC9y+RgYEBypUrh+XLl6Nz585ihEdEREREOoRJuQrOzs74559/YGNjI3YoRERERKSjmJQTEREREYmMPeVqOHXqFE6dOoX4+HjIZDKFfb6+viJFRURERES6gkm5CnPnzsW8efNQp04dlCxZkjcSIiIiIqJCx/YVFUqWLImlS5di0KBBYodCRERERDqK65SrkJWVhUaNGokdBhERERHpMCblKgwbNgw7duwQOwwiIiIi0mHsKVfh1atX2LBhA06ePAkPDw8YGBgo7F+xYoVIkRERERGRrmBPuQotWrTId59EIsHp06eLMBoiIiIi0kVMyomIiIiIRMaeciIiIiIikbGnXIUWLVp8cG1ytq8QERER0X/FpFyFGjVqKDzPzs7GjRs3EBISgiFDhogTFBERERHpFCblKqxcuVLp9u+++w7p6elFHA0RERER6SJO9PxIERERqFevHpKTk8UOhYiIiIi0HCd6fqSLFy/C2NhY7DCIiIiISAewfUWFHj16KDwXBAExMTG4evUqZs2aJVJURERERKRLmJSrYGFhofBcKpXCzc0N8+bNQ9u2bUWKioiIiIh0CXvKiYiIiIhExkq5mq5du4awsDAAQJUqVVCzZk2RIyIiIiIiXcGkXIX4+Hj07dsXZ86cgaWlJQAgNTUVLVq0wM6dO2FraytugERERESk9bj6igpjx47F8+fPERoaiuTkZCQnJyMkJATPnj3DuHHjxA6PiIiIiHQAe8pVsLCwwMmTJ1G3bl2F7VeuXEHbtm2RmpoqTmBEREREpDNYKVdBJpPBwMAgz3YDAwPIZDIRIiIiIiIiXcOkXIWWLVti/PjxePr0qXxbdHQ0JkyYgFatWokYGRERERHpCravqPD48WN07doVoaGhcHR0lG+rWrUqDh48iDJlyogcIRERERFpOyblahAEASdPnkR4eDgAoHLlymjdurXIURERERGRrmBSno/Tp09jzJgxuHTpEszNzRX2paWloVGjRli3bh2aNm0qUoREREREpCvYU56PVatWYfjw4XkScuD1iiwjR47EihUrRIiMiIiIiHQNk/J83Lx5E+3bt893f9u2bXHt2rUijIiIiIiIdBWT8nzExcUpXQrxX/r6+khISCjCiIiIiIhIVzEpz0fp0qUREhKS7/7g4GCULFmyCCMiIiIiIl3FpDwfHTt2xKxZs/Dq1as8+zIyMjBnzhx07txZhMiIiIiISNdw9ZV8xMXFoVatWtDT08OYMWPg5uYGAAgPD8fatWuRm5uLoKAg2NvbixwpEREREWk7JuUf8OjRI/j4+ODYsWP49zJJJBK0a9cOa9euhbOzs8gREhEREZEuYFKuhpSUFEREREAQBLi6usLKykrskIiIiIhIhzApJyIiIiISGSd6EhERERGJjEk5EREREZHImJQTEREREYmMSTkRERERkciYlBMRERERiYxJORERERGRyJiUExERERGJjEk5EREREZHI/g9ANHmCcs5lIwAAAABJRU5ErkJggg==\n"
          },
          "metadata": {}
        }
      ],
      "source": [
        "plt.figure(figsize=(8,8))\n",
        "sns.heatmap(weather_df_copy.corr(), annot=True);\n",
        "plt.tight_layout()"
      ]
    },
    {
      "cell_type": "markdown",
      "source": [
        "#APPLYING MODELS:"
      ],
      "metadata": {
        "id": "da_YnTRa2BOa"
      }
    },
    {
      "cell_type": "markdown",
      "source": [],
      "metadata": {
        "id": "5wA8HI9c9Vrr"
      }
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "gIe4IhfkuRlg"
      },
      "source": [
        "LINEAR REGRESSION"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 102,
      "metadata": {
        "id": "8MU9nMEC6ePZ"
      },
      "outputs": [],
      "source": [
        "from sklearn.model_selection import train_test_split\n",
        "from sklearn.linear_model import LinearRegression\n",
        "from sklearn.linear_model import SGDRegressor\n",
        "from sklearn.metrics import mean_absolute_error, mean_squared_error\n",
        "from sklearn.metrics import r2_score\n",
        "from sklearn import preprocessing"
      ]
    },
    {
      "cell_type": "markdown",
      "source": [
        "HERE, I AM PREDICTING AVERAGE TEMPERATURE AS I TRIED PREDICTING PRECIPITATION BUT IT IS GIVES HIGH ERROR"
      ],
      "metadata": {
        "id": "xWBsO9t8GGh6"
      }
    },
    {
      "cell_type": "code",
      "execution_count": 69,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "d5IxWsG_7o1w",
        "outputId": "8a400294-d7c3-4989-c3da-1c8868ed3913"
      },
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "MAE: 1.5994202914888749\n",
            "RMSE: 2.342296329438155\n",
            "R-squared (R²): 0.9472979228078706\n"
          ]
        }
      ],
      "source": [
        "X_train, X_test, y_train, y_test = train_test_split(weather_df_copy[[\"Country/Region\",\"Month\",\"PRCP\",\"TMIN\",\"TMAX\"]], weather_df_copy[\"TAVG\"], test_size=0.2)\n",
        "model = LinearRegression()\n",
        "model.fit(X_train, y_train)\n",
        "y_pred = model.predict(X_test)\n",
        "mae = mean_absolute_error(y_test, y_pred)\n",
        "rmse = np.sqrt(mean_squared_error(y_test, y_pred))\n",
        "r2 = r2_score(y_test, y_pred)\n",
        "\n",
        "print(f'MAE: {mae}')\n",
        "print(f'RMSE: {rmse}')\n",
        "print(f\"R-squared (R²): {r2}\")\n"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 70,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 564
        },
        "id": "jqMLVA_aWpTr",
        "outputId": "7b25e69c-3762-453c-b529-51d7079f7964"
      },
      "outputs": [
        {
          "output_type": "display_data",
          "data": {
            "text/plain": [
              "<Figure size 800x600 with 1 Axes>"
            ],
            "image/png": "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A336PAm5KhXw0UdAUhLg7CxraUREREQvAmd0la6yEvjrX4GlS/XLFgCgTRvgH/8AfH1lLY2IiIjoRWLQVbL8fGD6dP2sbbXhw/VPVuAsLhERESkcly4oWX4+8MMP+p8tLIDly4EjRxhyiYiIqElg0FWyPn2Azz7TPzLsu+/0a3KbNZO7KiIiIqKXgkFXSfLz9V8C8bQ5c4BLl/SPEyMiIiJqQhh0leLwYcDDA3j/fcNxlQrQamUpiYiIiEhODLrmrqICiIgAAgL0z8mNjgYOHpS7KiIiIiLZ8akL5uzWLWDKFP3X+VYLDAT69ZOvJiIiIiITwRldc3XggP7DZtUht3lz/WzuN98Ajo6ylkZERERkCjija250Ov1ShTVrnox17AjExwMDB8pXFxEREZGJYdA1J3fvAn/4A3Dq1JOxceOAbduAVq1kK4uIiIjIFHHpgjnRagEh9D9bWgIxMcBXXzHkEhEREdWCQdecWFnplyj07QucOAGEh+sfH0ZERERENXDpgin73/+AsjKgR48nY25uQFoaAy4RERHRr+CMrqn65z+BV18FJkwASksN9zHkEhEREf0qBl1TU1YGhIUBEycCxcVAdjawfLncVRERERGZHS5dMCVXrwKTJgGZmU/GpkwBPvpItpKIiIiIzBVndE3F7t36D5lVh1xra2DLFmDnTsDOTtbSiIiIiMwRZ3Tl9ugRMH8+8Pe/Pxlzdwf27gV695avLiIiIiIzx6Arp4oKYPBgICPjydibbwKxsYCtrXx1ERERESkAly7IqXlz4I039D/b2ABxccAXXzDkEhERERkBZ3TltmgRkJcHhIYaPi+XiIiIiBqFQVduFhbA2rVyV0FERESkOFy6QERERESKxKBLRERERIrEoEtEREREisSgS0RERESKxKBLRERERIrEoEtEREREisSgS0RERESKxKBLRERERIrEoEtEREREisSgS0RERESKxKBLRERERIrEoEtEREREisSgS0RERESKxKBLRERERIrEoEtEREREisSgS0RERESKxKBLRERERIrEoEtEREREitRc7gJMjRACAFBcXCxzJeZDp9Ph4cOHKC4uhqWlpdzlmCX20DjYR+NgHxuPPTQO9tE4lNjH6pxWnduehUH3F0pKSgAALi4uMldCRERERM9TUlICjUbzzP0q8WtRuImpqqpCXl4e7OzsoFKp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q6TzuLq6IiUlBbm5uVJQ9fHxwb179xAVFYUff/wRsbGxOHjwoMH1u3btii+//BKXL1/GqVOnMG3atAbNHtva2mLy5MmIiIjAnTt3MHPmTINrJCYm4sSJE7h8+TLeeustFBQUPPd8w4cPx/r165GRkYG0tDTMmTMHlpaW0v5p06bB0dERY8eOxbFjx3Dt2jUcPXoU4eHhuH37Nq5du4aIiAikpqbixo0bOHLkCK5evcp1ukTUaAy6RER1tHXrVvj6+hrMQlYLCgpCWloasrKy4OPjg4SEBHzzzTfo06cPhg8fbvDUguXLl+P69evo3Lmz9Kf77t27Y8OGDYiNjYWnpydOnz5t8KGw6usXFhaib9++mDFjBsLDw9G6desGvZeQkBAUFhbC39/fYBnGhx9+iL59+8Lf3x8+Pj5wdnbGuHHjnnuuNWvWwMXFBUOGDMHUqVOxaNEi2NjYSPttbGyQkpKCDh06YMKECejevTtCQkJQVlYGe3t72NjY4MqVKwgKCsJvf/tbhIaGIiwsDG+99VaD3hsRUTWV+OXCKiIiIiIiBeCMLhEREREpEoMuERERESkSgy4RERERKRKDLhEREREpEoMuERERESkSgy4RERERKRKDLhEREREpEoMuERERESkSgy4RERERKRKDLhEREREpEoMuERERESnS/wNicTcxcN0AEQAAAABJRU5ErkJggg==\n"
          },
          "metadata": {}
        }
      ],
      "source": [
        "plt.figure(figsize=(8, 6))\n",
        "plt.scatter(y_test, y_pred, alpha=0.5)\n",
        "plt.xlabel(\"Actual Values\")\n",
        "plt.ylabel(\"Predicted Values\")\n",
        "plt.title(\"Actual vs. Predicted Values\")\n",
        "plt.grid(True)\n",
        "\n",
        "# Add a diagonal line for reference (perfect predictions)\n",
        "plt.plot([min(y_test), max(y_test)], [min(y_test), max(y_test)], linestyle='--', color='red', linewidth=2)\n",
        "\n",
        "# Show the plot\n",
        "plt.show()"
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "size_scaler = preprocessing.StandardScaler().fit(X_train)\n",
        "X_train_scaled = size_scaler.transform(X_train)\n",
        "X_test_scaled = size_scaler.transform(X_test)\n",
        "X_train_scaled.shape, X_test_scaled.shape"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "2WF1Y0Jf9Sd4",
        "outputId": "3c1e776d-4c19-4867-fa7e-a85f698c3ca5"
      },
      "execution_count": 78,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "((1114060, 5), (278515, 5))"
            ]
          },
          "metadata": {},
          "execution_count": 78
        }
      ]
    },
    {
      "cell_type": "markdown",
      "source": [
        "LASSO REGRESSION"
      ],
      "metadata": {
        "id": "OkBBkpH42LQw"
      }
    },
    {
      "cell_type": "code",
      "source": [
        "from sklearn.linear_model import Lasso"
      ],
      "metadata": {
        "id": "4SgZCm6arMp9"
      },
      "execution_count": 79,
      "outputs": []
    },
    {
      "cell_type": "code",
      "execution_count": 110,
      "metadata": {
        "id": "DDbxi0-DaXrG",
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "outputId": "df77c2a7-480a-4790-834f-80b81d543251"
      },
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "MSE for Lasso Regression 6.619688028486198\n",
            "MAE: 1.5994202914888749\n",
            "RMSE: 10.20314505317143\n",
            "R-squared (R²): -2.80431325767605e-05\n"
          ]
        }
      ],
      "source": [
        "#Lasso Regression\n",
        "model2 = Lasso(alpha=1.0)\n",
        "model2.fit(X_train_scaled, y_train)\n",
        "y_pred2 = model2.predict(X_test_scaled)\n",
        "mse2 = mean_squared_error(y_test, y_pred2)\n",
        "print(\"MSE for Lasso Regression\",mse2)\n",
        "mae2 = mean_absolute_error(y_test, y_pred2)\n",
        "rmse2 = np.sqrt(mean_squared_error(y_test, y_pred))\n",
        "r22 = r2_score(y_test, y_pred)\n",
        "\n",
        "print(f'MAE: {mae}')\n",
        "print(f'RMSE: {rmse2}')\n",
        "print(f\"R-squared (R²): {r22}\")\n"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 111,
      "metadata": {
        "id": "0MpQmmoJadOl",
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "outputId": "fbed2f00-e63b-4163-819f-a07981791f45"
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "{'alpha': 1.0,\n",
              " 'copy_X': True,\n",
              " 'fit_intercept': True,\n",
              " 'max_iter': 1000,\n",
              " 'positive': False,\n",
              " 'precompute': False,\n",
              " 'random_state': None,\n",
              " 'selection': 'cyclic',\n",
              " 'tol': 0.0001,\n",
              " 'warm_start': False}"
            ]
          },
          "metadata": {},
          "execution_count": 111
        }
      ],
      "source": [
        "model2.get_params()"
      ]
    },
    {
      "cell_type": "code",
      "source": [],
      "metadata": {
        "id": "MviMEAWKLxA0"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [
        "from sklearn.model_selection import GridSearchCV\n",
        "\n",
        "model=Lasso()\n",
        "param_grid = {\n",
        "    'alpha': [0.001, 0.01, 0.1, 1, 10, 100],\n",
        "    'fit_intercept': [True, False],\n",
        "    'max_iter': [100,200,300,500,700,1000],\n",
        "    'positive': [True,False]\n",
        "}\n",
        "\n",
        "grid_search = GridSearchCV(model, param_grid, cv=5,verbose=1, n_jobs=-1)\n",
        "grid_search.fit(X_train_scaled, y_train)\n",
        "best_params_Lasso = grid_search.best_params_\n",
        "print(f\"Best parameters: {best_params_Lasso}\")\n",
        "\n",
        "best_model = grid_search.best_estimator_\n",
        "test_score = best_model.score(X_test_scaled, y_test)\n",
        "print(f\"Test R^2 Score of Best Model: {test_score}\")\n",
        "\n"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 894
        },
        "id": "GDlCQEgmWylJ",
        "outputId": "67498774-e5dd-4cff-8676-588005f512ef"
      },
      "execution_count": 125,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "Fitting 5 folds for each of 144 candidates, totalling 720 fits\n"
          ]
        },
        {
          "output_type": "error",
          "ename": "PicklingError",
          "evalue": "ignored",
          "traceback": [
            "\u001b[0;31m---------------------------------------------------------------------------\u001b[0m",
            "\u001b[0;31m_RemoteTraceback\u001b[0m                          Traceback (most recent call last)",
            "\u001b[0;31m_RemoteTraceback\u001b[0m: \n\"\"\"\nTraceback (most recent call last):\n  File \"/usr/local/lib/python3.10/dist-packages/joblib/externals/loky/backend/queues.py\", line 159, in _feed\n    obj_ = dumps(obj, reducers=reducers)\n  File \"/usr/local/lib/python3.10/dist-packages/joblib/externals/loky/backend/reduction.py\", line 215, in dumps\n    dump(obj, buf, reducers=reducers, protocol=protocol)\n  File \"/usr/local/lib/python3.10/dist-packages/joblib/externals/loky/backend/reduction.py\", line 208, in dump\n    _LokyPickler(file, reducers=reducers, protocol=protocol).dump(obj)\n  File \"/usr/local/lib/python3.10/dist-packages/joblib/externals/cloudpickle/cloudpickle_fast.py\", line 632, in dump\n    return Pickler.dump(self, obj)\n  File \"/usr/local/lib/python3.10/dist-packages/joblib/_memmapping_reducer.py\", line 446, in __call__\n    for dumped_filename in dump(a, filename):\n  File \"/usr/local/lib/python3.10/dist-packages/joblib/numpy_pickle.py\", line 553, in dump\n    NumpyPickler(f, protocol=protocol).dump(value)\n  File \"/usr/lib/python3.10/pickle.py\", line 487, in dump\n    self.save(obj)\n  File \"/usr/local/lib/python3.10/dist-packages/joblib/numpy_pickle.py\", line 352, in save\n    wrapper.write_array(obj, self)\n  File \"/usr/local/lib/python3.10/dist-packages/joblib/numpy_pickle.py\", line 134, in write_array\n    pickler.file_handle.write(chunk.tobytes('C'))\nOSError: [Errno 28] No space left on device\n\"\"\"",
            "\nThe above exception was the direct cause of the following exception:\n",
            "\u001b[0;31mPicklingError\u001b[0m                             Traceback (most recent call last)",
            "\u001b[0;32m<ipython-input-125-05bc7098c795>\u001b[0m in \u001b[0;36m<cell line: 12>\u001b[0;34m()\u001b[0m\n\u001b[1;32m     10\u001b[0m \u001b[0;34m\u001b[0m\u001b[0m\n\u001b[1;32m     11\u001b[0m \u001b[0mgrid_search\u001b[0m \u001b[0;34m=\u001b[0m \u001b[0mGridSearchCV\u001b[0m\u001b[0;34m(\u001b[0m\u001b[0mmodel\u001b[0m\u001b[0;34m,\u001b[0m \u001b[0mparam_grid\u001b[0m\u001b[0;34m,\u001b[0m \u001b[0mcv\u001b[0m\u001b[0;34m=\u001b[0m\u001b[0;36m5\u001b[0m\u001b[0;34m,\u001b[0m\u001b[0mverbose\u001b[0m\u001b[0;34m=\u001b[0m\u001b[0;36m1\u001b[0m\u001b[0;34m,\u001b[0m \u001b[0mn_jobs\u001b[0m\u001b[0;34m=\u001b[0m\u001b[0;34m-\u001b[0m\u001b[0;36m1\u001b[0m\u001b[0;34m)\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[0;32m---> 12\u001b[0;31m \u001b[0mgrid_search\u001b[0m\u001b[0;34m.\u001b[0m\u001b[0mfit\u001b[0m\u001b[0;34m(\u001b[0m\u001b[0mX_train_scaled\u001b[0m\u001b[0;34m,\u001b[0m \u001b[0my_train\u001b[0m\u001b[0;34m)\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[0m\u001b[1;32m     13\u001b[0m \u001b[0mbest_params_Lasso\u001b[0m \u001b[0;34m=\u001b[0m \u001b[0mgrid_search\u001b[0m\u001b[0;34m.\u001b[0m\u001b[0mbest_params_\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[1;32m     14\u001b[0m \u001b[0mprint\u001b[0m\u001b[0;34m(\u001b[0m\u001b[0;34mf\"Best parameters: {best_params_Lasso}\"\u001b[0m\u001b[0;34m)\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n",
            "\u001b[0;32m/usr/local/lib/python3.10/dist-packages/sklearn/model_selection/_search.py\u001b[0m in \u001b[0;36mfit\u001b[0;34m(self, X, y, groups, **fit_params)\u001b[0m\n\u001b[1;32m    872\u001b[0m                 \u001b[0;32mreturn\u001b[0m \u001b[0mresults\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[1;32m    873\u001b[0m \u001b[0;34m\u001b[0m\u001b[0m\n\u001b[0;32m--> 874\u001b[0;31m             \u001b[0mself\u001b[0m\u001b[0;34m.\u001b[0m\u001b[0m_run_search\u001b[0m\u001b[0;34m(\u001b[0m\u001b[0mevaluate_candidates\u001b[0m\u001b[0;34m)\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[0m\u001b[1;32m    875\u001b[0m \u001b[0;34m\u001b[0m\u001b[0m\n\u001b[1;32m    876\u001b[0m             \u001b[0;31m# multimetric is determined here because in the case of a callable\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n",
            "\u001b[0;32m/usr/local/lib/python3.10/dist-packages/sklearn/model_selection/_search.py\u001b[0m in \u001b[0;36m_run_search\u001b[0;34m(self, evaluate_candidates)\u001b[0m\n\u001b[1;32m   1386\u001b[0m     \u001b[0;32mdef\u001b[0m \u001b[0m_run_search\u001b[0m\u001b[0;34m(\u001b[0m\u001b[0mself\u001b[0m\u001b[0;34m,\u001b[0m \u001b[0mevaluate_candidates\u001b[0m\u001b[0;34m)\u001b[0m\u001b[0;34m:\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[1;32m   1387\u001b[0m         \u001b[0;34m\"\"\"Search all candidates in param_grid\"\"\"\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[0;32m-> 1388\u001b[0;31m         \u001b[0mevaluate_candidates\u001b[0m\u001b[0;34m(\u001b[0m\u001b[0mParameterGrid\u001b[0m\u001b[0;34m(\u001b[0m\u001b[0mself\u001b[0m\u001b[0;34m.\u001b[0m\u001b[0mparam_grid\u001b[0m\u001b[0;34m)\u001b[0m\u001b[0;34m)\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[0m\u001b[1;32m   1389\u001b[0m \u001b[0;34m\u001b[0m\u001b[0m\n\u001b[1;32m   1390\u001b[0m \u001b[0;34m\u001b[0m\u001b[0m\n",
            "\u001b[0;32m/usr/local/lib/python3.10/dist-packages/sklearn/model_selection/_search.py\u001b[0m in \u001b[0;36mevaluate_candidates\u001b[0;34m(candidate_params, cv, more_results)\u001b[0m\n\u001b[1;32m    819\u001b[0m                     )\n\u001b[1;32m    820\u001b[0m \u001b[0;34m\u001b[0m\u001b[0m\n\u001b[0;32m--> 821\u001b[0;31m                 out = parallel(\n\u001b[0m\u001b[1;32m    822\u001b[0m                     delayed(_fit_and_score)(\n\u001b[1;32m    823\u001b[0m                         \u001b[0mclone\u001b[0m\u001b[0;34m(\u001b[0m\u001b[0mbase_estimator\u001b[0m\u001b[0;34m)\u001b[0m\u001b[0;34m,\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n",
            "\u001b[0;32m/usr/local/lib/python3.10/dist-packages/sklearn/utils/parallel.py\u001b[0m in \u001b[0;36m__call__\u001b[0;34m(self, iterable)\u001b[0m\n\u001b[1;32m     61\u001b[0m             \u001b[0;32mfor\u001b[0m \u001b[0mdelayed_func\u001b[0m\u001b[0;34m,\u001b[0m \u001b[0margs\u001b[0m\u001b[0;34m,\u001b[0m \u001b[0mkwargs\u001b[0m \u001b[0;32min\u001b[0m \u001b[0miterable\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[1;32m     62\u001b[0m         )\n\u001b[0;32m---> 63\u001b[0;31m         \u001b[0;32mreturn\u001b[0m \u001b[0msuper\u001b[0m\u001b[0;34m(\u001b[0m\u001b[0;34m)\u001b[0m\u001b[0;34m.\u001b[0m\u001b[0m__call__\u001b[0m\u001b[0;34m(\u001b[0m\u001b[0miterable_with_config\u001b[0m\u001b[0;34m)\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[0m\u001b[1;32m     64\u001b[0m \u001b[0;34m\u001b[0m\u001b[0m\n\u001b[1;32m     65\u001b[0m \u001b[0;34m\u001b[0m\u001b[0m\n",
            "\u001b[0;32m/usr/local/lib/python3.10/dist-packages/joblib/parallel.py\u001b[0m in \u001b[0;36m__call__\u001b[0;34m(self, iterable)\u001b[0m\n\u001b[1;32m   1950\u001b[0m         \u001b[0mnext\u001b[0m\u001b[0;34m(\u001b[0m\u001b[0moutput\u001b[0m\u001b[0;34m)\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[1;32m   1951\u001b[0m \u001b[0;34m\u001b[0m\u001b[0m\n\u001b[0;32m-> 1952\u001b[0;31m         \u001b[0;32mreturn\u001b[0m \u001b[0moutput\u001b[0m \u001b[0;32mif\u001b[0m \u001b[0mself\u001b[0m\u001b[0;34m.\u001b[0m\u001b[0mreturn_generator\u001b[0m \u001b[0;32melse\u001b[0m \u001b[0mlist\u001b[0m\u001b[0;34m(\u001b[0m\u001b[0moutput\u001b[0m\u001b[0;34m)\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[0m\u001b[1;32m   1953\u001b[0m \u001b[0;34m\u001b[0m\u001b[0m\n\u001b[1;32m   1954\u001b[0m     \u001b[0;32mdef\u001b[0m \u001b[0m__repr__\u001b[0m\u001b[0;34m(\u001b[0m\u001b[0mself\u001b[0m\u001b[0;34m)\u001b[0m\u001b[0;34m:\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n",
            "\u001b[0;32m/usr/local/lib/python3.10/dist-packages/joblib/parallel.py\u001b[0m in \u001b[0;36m_get_outputs\u001b[0;34m(self, iterator, pre_dispatch)\u001b[0m\n\u001b[1;32m   1593\u001b[0m \u001b[0;34m\u001b[0m\u001b[0m\n\u001b[1;32m   1594\u001b[0m             \u001b[0;32mwith\u001b[0m \u001b[0mself\u001b[0m\u001b[0;34m.\u001b[0m\u001b[0m_backend\u001b[0m\u001b[0;34m.\u001b[0m\u001b[0mretrieval_context\u001b[0m\u001b[0;34m(\u001b[0m\u001b[0;34m)\u001b[0m\u001b[0;34m:\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[0;32m-> 1595\u001b[0;31m                 \u001b[0;32myield\u001b[0m \u001b[0;32mfrom\u001b[0m \u001b[0mself\u001b[0m\u001b[0;34m.\u001b[0m\u001b[0m_retrieve\u001b[0m\u001b[0;34m(\u001b[0m\u001b[0;34m)\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[0m\u001b[1;32m   1596\u001b[0m \u001b[0;34m\u001b[0m\u001b[0m\n\u001b[1;32m   1597\u001b[0m         \u001b[0;32mexcept\u001b[0m \u001b[0mGeneratorExit\u001b[0m\u001b[0;34m:\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n",
            "\u001b[0;32m/usr/local/lib/python3.10/dist-packages/joblib/parallel.py\u001b[0m in \u001b[0;36m_retrieve\u001b[0;34m(self)\u001b[0m\n\u001b[1;32m   1697\u001b[0m             \u001b[0;31m# worker traceback.\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[1;32m   1698\u001b[0m             \u001b[0;32mif\u001b[0m \u001b[0mself\u001b[0m\u001b[0;34m.\u001b[0m\u001b[0m_aborting\u001b[0m\u001b[0;34m:\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[0;32m-> 1699\u001b[0;31m                 \u001b[0mself\u001b[0m\u001b[0;34m.\u001b[0m\u001b[0m_raise_error_fast\u001b[0m\u001b[0;34m(\u001b[0m\u001b[0;34m)\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[0m\u001b[1;32m   1700\u001b[0m                 \u001b[0;32mbreak\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[1;32m   1701\u001b[0m \u001b[0;34m\u001b[0m\u001b[0m\n",
            "\u001b[0;32m/usr/local/lib/python3.10/dist-packages/joblib/parallel.py\u001b[0m in \u001b[0;36m_raise_error_fast\u001b[0;34m(self)\u001b[0m\n\u001b[1;32m   1732\u001b[0m         \u001b[0;31m# called directly or if the generator is gc'ed.\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[1;32m   1733\u001b[0m         \u001b[0;32mif\u001b[0m \u001b[0merror_job\u001b[0m \u001b[0;32mis\u001b[0m \u001b[0;32mnot\u001b[0m \u001b[0;32mNone\u001b[0m\u001b[0;34m:\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[0;32m-> 1734\u001b[0;31m             \u001b[0merror_job\u001b[0m\u001b[0;34m.\u001b[0m\u001b[0mget_result\u001b[0m\u001b[0;34m(\u001b[0m\u001b[0mself\u001b[0m\u001b[0;34m.\u001b[0m\u001b[0mtimeout\u001b[0m\u001b[0;34m)\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[0m\u001b[1;32m   1735\u001b[0m \u001b[0;34m\u001b[0m\u001b[0m\n\u001b[1;32m   1736\u001b[0m     \u001b[0;32mdef\u001b[0m \u001b[0m_warn_exit_early\u001b[0m\u001b[0;34m(\u001b[0m\u001b[0mself\u001b[0m\u001b[0;34m)\u001b[0m\u001b[0;34m:\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n",
            "\u001b[0;32m/usr/local/lib/python3.10/dist-packages/joblib/parallel.py\u001b[0m in \u001b[0;36mget_result\u001b[0;34m(self, timeout)\u001b[0m\n\u001b[1;32m    734\u001b[0m             \u001b[0;31m# callback thread, and is stored internally. It's just waiting to\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[1;32m    735\u001b[0m             \u001b[0;31m# be returned.\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[0;32m--> 736\u001b[0;31m             \u001b[0;32mreturn\u001b[0m \u001b[0mself\u001b[0m\u001b[0;34m.\u001b[0m\u001b[0m_return_or_raise\u001b[0m\u001b[0;34m(\u001b[0m\u001b[0;34m)\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[0m\u001b[1;32m    737\u001b[0m \u001b[0;34m\u001b[0m\u001b[0m\n\u001b[1;32m    738\u001b[0m         \u001b[0;31m# For other backends, the main thread needs to run the retrieval step.\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n",
            "\u001b[0;32m/usr/local/lib/python3.10/dist-packages/joblib/parallel.py\u001b[0m in \u001b[0;36m_return_or_raise\u001b[0;34m(self)\u001b[0m\n\u001b[1;32m    752\u001b[0m         \u001b[0;32mtry\u001b[0m\u001b[0;34m:\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[1;32m    753\u001b[0m             \u001b[0;32mif\u001b[0m \u001b[0mself\u001b[0m\u001b[0;34m.\u001b[0m\u001b[0mstatus\u001b[0m \u001b[0;34m==\u001b[0m \u001b[0mTASK_ERROR\u001b[0m\u001b[0;34m:\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[0;32m--> 754\u001b[0;31m                 \u001b[0;32mraise\u001b[0m \u001b[0mself\u001b[0m\u001b[0;34m.\u001b[0m\u001b[0m_result\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[0m\u001b[1;32m    755\u001b[0m             \u001b[0;32mreturn\u001b[0m \u001b[0mself\u001b[0m\u001b[0;34m.\u001b[0m\u001b[0m_result\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[1;32m    756\u001b[0m         \u001b[0;32mfinally\u001b[0m\u001b[0;34m:\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n",
            "\u001b[0;31mPicklingError\u001b[0m: Could not pickle the task to send it to the workers."
          ]
        }
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 117,
      "metadata": {
        "id": "w-bbYSowaiaD",
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "outputId": "8b8753b0-aebb-4d95-9a5f-ff7919e4aa0d"
      },
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "5.558727170135954\n",
            "MAE: 1.6219886196814912\n",
            "RMSE: 10.20314505317143\n"
          ]
        }
      ],
      "source": [
        "##Lasso tunning\n",
        "model2t=Lasso(alpha= 0.001, fit_intercept= True, max_iter= 100, positive= True)\n",
        "model2t.fit(X_train,y_train)\n",
        "y_predt2=model2t.predict(X_test)\n",
        "mse2t = mean_squared_error(y_test, y_predt2)\n",
        "print(mse2t)\n",
        "mae4 = mean_absolute_error(y_test, y_predt2)\n",
        "rmse4 = np.sqrt(mean_squared_error(y_test, y_pred))\n",
        "\n",
        "\n",
        "print(f'MAE: {mae4}')\n",
        "print(f'RMSE: {rmse4}')\n",
        "\n"
      ]
    },
    {
      "cell_type": "markdown",
      "source": [
        "RIDGE REGRESSION"
      ],
      "metadata": {
        "id": "FTiyIMJy2Wf8"
      }
    },
    {
      "cell_type": "code",
      "source": [
        "from sklearn.linear_model import Ridge"
      ],
      "metadata": {
        "id": "QN96bXq-Dcop"
      },
      "execution_count": 93,
      "outputs": []
    },
    {
      "cell_type": "code",
      "execution_count": 119,
      "metadata": {
        "id": "i7vKwb2GalVh",
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "outputId": "00cd7ccd-62d9-46e7-9033-a9377cf852d6"
      },
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "5.486352093434954\n",
            "MAE: 1.5994202829978572\n",
            "RMSE: 10.20314505317143\n"
          ]
        }
      ],
      "source": [
        "#Ridge Regression\n",
        "model3 = Ridge()\n",
        "model3.fit(X_train, y_train)\n",
        "y_pred3 = model3.predict(X_test)\n",
        "mse3 = mean_squared_error(y_test, y_pred3)\n",
        "print(mse3)\n",
        "mae3 = mean_absolute_error(y_test, y_pred3)\n",
        "rmse3 = np.sqrt(mean_squared_error(y_test, y_pred))\n",
        "\n",
        "\n",
        "print(f'MAE: {mae3}')\n",
        "print(f'RMSE: {rmse3}')\n",
        "\n"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 95,
      "metadata": {
        "id": "T93VNLRtaqEW",
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "outputId": "92f6117d-45a8-4d5d-cc81-53e8c7873529"
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "{'alpha': 1.0,\n",
              " 'copy_X': True,\n",
              " 'fit_intercept': True,\n",
              " 'max_iter': None,\n",
              " 'positive': False,\n",
              " 'random_state': None,\n",
              " 'solver': 'auto',\n",
              " 'tol': 0.0001}"
            ]
          },
          "metadata": {},
          "execution_count": 95
        }
      ],
      "source": [
        "model3.get_params()"
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "print('Linear regression:')\n",
        "print(f'MAE: {mae}')\n",
        "print(f'RMSE: {rmse}')\n",
        "print(f\"R-squared (R²): {r2}\")"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "cyNZIM6bIc_a",
        "outputId": "155491d4-c801-43de-d396-65377fdd07c4"
      },
      "execution_count": 121,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "Linear regression:\n",
            "MAE: 1.5994202914888749\n",
            "RMSE: 2.342296329438155\n",
            "R-squared (R²): 0.9472979228078706\n"
          ]
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "print('Lasso regression:')\n",
        "print(f'MAE: {mae2t}')\n",
        "print(f'RMSE: {rmse4}')\n"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "ieAy3ZK4KAJy",
        "outputId": "6472fd2a-80aa-4ffc-f343-86c9e25f9ab7"
      },
      "execution_count": 124,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "Lasso regression:\n",
            "MAE: 1.6219886196814912\n",
            "RMSE: 10.20314505317143\n"
          ]
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "print('Ridge regression:')\n",
        "print(f'MAE: {mae3}')\n",
        "print(f'RMSE: {rmse3}')\n"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "X5yueAl9KAwc",
        "outputId": "55610b83-005f-43fb-f23f-b58aba352b47"
      },
      "execution_count": 123,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "Ridge regression:\n",
            "MAE: 1.5994202829978572\n",
            "RMSE: 10.20314505317143\n"
          ]
        }
      ]
    },
    {
      "cell_type": "markdown",
      "source": [
        "In above obervations it can be seen that we have got quite high error for all models.This is due to the dataset.As out dataset was having so many empty values it was tough to predict the TAVG afer dropping so many columns and filling so many null values"
      ],
      "metadata": {
        "id": "imaUUeBfH6kP"
      }
    }
  ],
  "metadata": {
    "colab": {
      "provenance": [],
      "include_colab_link": true
    },
    "kernelspec": {
      "display_name": "Python 3",
      "name": "python3"
    },
    "language_info": {
      "name": "python"
    }
  },
  "nbformat": 4,
  "nbformat_minor": 0
}