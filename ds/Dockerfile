FROM jupyter/scipy-notebook

RUN pip install --upgrade pip && \
    pip install --no-cache-dir \
        'geopandas' \
        'folium' \
        'ipyleaflet' \
        'plotly' \
        'partridge[full]' \
        'modin[all]' \
        'jupyter_contrib_nbextensions' \
        'cudf-cuda100'

RUN jupyter contrib nbextension install --sys-prefix
