# Recette Hugo Rapide

Pour test over katacoda

```bash 
# --- HUGO PROJECT
# --- FOR THE OMEGA PROJECT'S
# --- GITHUB PAGES SPECIFICS
# -------------------------
# echo " C'est là qu'on trouvera par exemple le config.toml, etc..."
# echo " That's where we'll find versioned all Hugo Project's Files like the [config.toml]"
export HUGO_PROJECT_GIT_URI=git@gitlab.com:second-bureau/omega.io/github-pages/hugo-generator.git
# echo " That's the repo where the Github PAGES are activated, serving master content, or master [./docs] folder content"
export GITHUB_PAGES_DEPLOYMENT_GIT_REPO_URI=git@github.com:Jean-Baptiste-Lasselle/omega.git

# The Pipeline automating all operations to build and deploy Omega's gfithub Pages :
# => Initializing a new Hugo PROJECT
# => Resuming an existing Hugo Project.

export OMEGA_GITHUB_PAGES_PIPELINE_IAAC_GIT_URI=git@gitlab.com:second-bureau/omega.git


export URI_DE_CE_REPO=$OMEGA_GITHUB_PAGES_PIPELINE_IAAC_GIT_URI


export MESSAGE_COMMIT=""
export MESSAGE_COMMIT="$MESSAGE_COMMIT Mon message de commit".

export OPS_HOME=~/.OMEGA_GU_PAGES_HUGO_TEMP_WORK

mkdir -p $OPS_HOME
cd $OPS_HOME
echo "[GIT_SSH_COMMAND=$GIT_SSH_COMMAND]"
git clone "$URI_DE_CE_REPO" .
git add --all && git commit -m "MESSAGE_COMMIT" && git push

chmod +x ./operations.sh
./operations.sh
```
