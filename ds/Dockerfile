FROM jupyter/minimal-notebook

USER root

# ffmpeg for matplotlib anim
RUN apt-get update && \
    apt-get install -y --no-install-recommends ffmpeg && \
    rm -rf /var/lib/apt/lists/*

USER $NB_UID



RUN pip install --upgrade pip && \
    pip install --no-cache-dir \
        'bokeh' \
        'cudf-cuda100' \
        'folium' \
        'geopandas' \
        'ipyleaflet' \
        'ipywidgets' \
        'jupyterlab-dash' \
        'matplotlib' \
        'plotly' \
        'partridge[full]' \
        'autopep8' \
        'modin[ray]' \
        'jupyter_contrib_nbextensions' \
        'widgetsnbextension'

# Activate ipywidgets extension in the environment that runs the notebook server
RUN jupyter nbextension enable --py widgetsnbextension --sys-prefix && \
    # Also activate ipywidgets extension for JupyterLab
    # Check this URL for most recent compatibilities
    # https://github.com/jupyter-widgets/ipywidgets/tree/master/packages/jupyterlab-manager
    jupyter labextension install @jupyter-widgets/jupyterlab-manager@^1.1.0 --no-build && \
    jupyter labextension install jupyterlab_bokeh@1.0.0 --no-build && \
    jupyter labextension install jupyter-matplotlib --no-build && \
    jupyter lab build && \
    jupyter contrib nbextension install --sys-prefix && \
    jupyter labextension install jupyterlab-dash \
    npm cache clean --force && \
    rm -rf $CONDA_DIR/share/jupyter/lab/staging && \
    rm -rf /home/$NB_USER/.cache/yarn && \
    rm -rf /home/$NB_USER/.node-gyp && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER

# Import matplotlib the first time to build the font cache.
ENV XDG_CACHE_HOME /home/$NB_USER/.cache/
RUN MPLBACKEND=Agg python -c "import matplotlib.pyplot" && \
    fix-permissions /home/$NB_USER
