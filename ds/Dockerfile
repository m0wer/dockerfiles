FROM jupyter/minimal-notebook

USER root

# R pre-requisites
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    fonts-dejavu \
    gfortran \
    gcc && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# ffmpeg for matplotlib anim
RUN apt-get update && \
    apt-get install -y --no-install-recommends ffmpeg \
                                               graphviz \
                                               openjdk-8-jdk && \
    rm -rf /var/lib/apt/lists/*

USER $NB_UID

# R packages including IRKernel which gets installed globally.
RUN conda install --quiet --yes \
    'r-base=4.0.3'  \
    'r-caret=6.0*' \
    'r-crayon=1.4*' \
    'r-devtools=2.3*' \
    'r-forecast=8.13*' \ 
    'r-hexbin=1.28*' \
    'r-htmltools=0.5*' \
    'r-htmlwidgets=1.5*' \ 
    'r-irkernel=1.1*' \
    'r-nycflights13=1.0*' \
    'r-randomforest=4.6*' \
    'r-rcurl=1.98*' \
    'r-rmarkdown=2.7*' \
    'r-rsqlite=2.2*' \
    'r-shiny=1.6*' \
    'r-tidyverse=1.3*' \
    'rpy2=3.4*' && \
    conda clean --all -f -y && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

RUN pip install --upgrade pip && \
    pip install --no-cache-dir \
        'ipywidgets' \
        'jupyter_contrib_nbextensions' \
        'matplotlib' \
        'widgetsnbextension'

# Activate ipywidgets extension in the environment that runs the notebook server
RUN jupyter nbextension enable --py widgetsnbextension --sys-prefix && \
    # Also activate ipywidgets extension for JupyterLab
    # Check this URL for most recent compatibilities
    # https://github.com/jupyter-widgets/ipywidgets/tree/master/packages/jupyterlab-manager
    jupyter labextension install @jupyter-widgets/jupyterlab-manager --no-build && \
    #jupyter labextension install @bokeh/jupyter_bokeh --no-build && \
    # jupyter labextension install jupyter-matplotlib --no-build && \
    jupyter lab build --dev-build=False && \
    jupyter contrib nbextension install --sys-prefix && \
    #jupyter labextension install jupyterlab-dash && \
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

RUN pip install --upgrade pip && \
    pip install --no-cache-dir \
        'scikit-learn'

RUN pip install --no-cache-dir \
        'autopep8' \
        'bokeh' \
        'git+git://github.com/cgupm/crtm_poll' \
        'dask' \
        'folium' \
        'gdown' \
        'geopandas' \
        'geopy' \
        'graphviz' \
        'ipyleaflet' \
        'isort' \
        'jupyterlab-dash' \
        'kaleido' \
        'mlinsights' \
        'modin[ray]' \
        'mrjob' \
        'pandarallel' \
        'partridge[full]' \
        'plotly' \
        'psutil' \
        'psycopg2-binary' \
        'pyquickhelper' \
        'pyspark' \
        'seaborn' \
        'SimpSOM' \
        'sqlalchemy' \
        'statsmodels' \
        'sympy' \
        'xgboost'
