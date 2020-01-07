FROM jupyter/scipy-notebook

# Install Python 3 packages
RUN conda install --quiet --yes \
    'geopandas' \
    'folium' \
    'ipyleaflet'

RUN conda install --quiet --yes \
    -c rapidsai cudf
 
 
RUN pip install --upgrade pip && \
    pip install --no-cache-dir \
        'partridge[full]' \
        'modin'
