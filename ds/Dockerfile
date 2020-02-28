FROM jupyter/scipy-notebook

RUN pip install --upgrade pip && \
    pip install --no-cache-dir \
        'geopandas' \
        'folium' \
        'ipyleaflet' \
        'jupyterlab-dash' \
        'plotly' \
        'partridge[full]' \
        'autopep8' \
        'modin[all]' \
        'jupyter_contrib_nbextensions' \
        'cudf-cuda100'

RUN jupyter contrib nbextension install --sys-prefix
RUN jupyter labextension install jupyterlab-dash --sys-prefix
