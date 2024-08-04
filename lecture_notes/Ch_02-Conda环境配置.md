### Conda环境配置（Windows系统）

Conda是一个开源的包管理器和环境管理器，可以用于安装、运行和更新包和其依赖。Conda可以管理不同版本的软件包和环境，以便用户在不同的项目中使用不同的软件包和Python版本，而不会产生冲突。

1. **创建Conda环境**
   创建一个新的Conda环境非常简单。你可以使用以下命令来创建一个新的环境，其中 `myenv`是你想要创建的环境的名称，`python=3.8`指定了Python的版本：

   ```bash
   conda create --name myenv python=3.8

   #克隆环境
   conda create --name newenv --clone oldenv
   ```

   这个命令会在Conda的环境中创建一个名为 `myenv`的新环境，**并安装指定版本的Python**。
2. **激活Conda环境**
   一旦你创建了一个环境，你可以通过以下命令来激活它：

   ```bash
   conda activate myenv
   ```

   这个命令会激活名为 `myenv`的环境。一旦环境被激活，你所有的Conda命令都将在这个环境中执行。

   在当前已激活的环境中安装指定包

   ```bash
   conda install numpy
   ```

3. **退出Conda环境**
   如果你想退出当前激活的环境并返回到基础环境，可以使用以下命令：

   ```bash
   conda deactivate
   ```

   这个命令会将你的shell状态设置回基础环境，你可以在其中切换到其他环境或者直接使用系统级别的Python。
4. **销毁Conda环境**
   如果你确定不再需要一个环境，可以使用以下命令来删除它：

   ```bash
   conda env remove --name myenv
   ```

   这个命令会删除名为 `myenv`的环境及其包含的所有软件包。
5. **使用Conda管理多个Python版本和依赖**
   查看已安装的环境列表

   ```bash
   conda env list
   ```

   Conda不仅可以创建和管理环境，还可以在同一系统中安装和管理多个Python版本。例如，如果你想安装Python 3.6和Python 3.8，可以创建两个不同的环境：

   ```bash
   conda create --name py36 python=3.6
   conda create --name py38 python=3.8
   ```

   然后，你可以通过 `conda activate`命令在这两个环境之间切换，以使用不同版本的Python。
   对于依赖管理，Conda可以自动处理大多数依赖关系。当你使用 `conda install`命令安装一个包时，Conda会自动安装该包所需的所有依赖项。同样，当你更新或删除一个包时，Conda也会自动处理依赖项的更新或删除。
   此外，Conda还可以使用 `requirements.txt`文件或 `environment.yml`文件来管理依赖。这些文件列出了环境中所需的所有软件包及其版本。
   通过使用Conda，你可以轻松地在不同的项目之间切换，每个项目都可以有自己的环境和依赖，从而避免版本冲突和依赖问题。

### 查看Anaconda中的Python版本

要查看Anaconda中默认安装的Python版本，或者查看某个特定Conda环境中安装的Python版本，你可以使用以下方法：

1. **查看默认Python版本**：
   如果你想要查看Anaconda安装后默认使用的Python版本，你可以打开Anaconda Prompt（在Windows上）或者终端（在macOS和Linux上），然后输入以下命令：

   ```bash
   conda --version
   ```

   这个命令会显示conda的版本信息以及默认Python的版本。
2. **查看特定环境中的Python版本**：
   如果你已经创建了一个或多个Conda环境，并想知道这些环境中安装的Python版本，你可以首先激活相应的环境，然后使用以下命令：

   ```bash
   python --version
   ```

   或者，你也可以使用conda命令来查看环境中安装的所有包及其版本，包括Python：

   ```bash
   conda list
   ```

这个命令会列出当前环境中所有已安装的包，你可以通过查找 `python`条目来确定安装的Python版本。

3. **查看所有环境中的Python版本**：
   如果你想查看Anaconda中所有环境的Python版本，你可以使用以下命令：

   ```bash
   conda env list
   ```

这个命令会列出所有环境及其配置，包括每个环境使用的Python版本。

通过上述方法，你可以轻松地查看Anaconda中安装的Python版本，无论是默认环境还是特定的Conda环境。这有助于你了解当前的开发环境，并确保你使用的是正确的Python版本来进行开发工作。

### 使用conda和pip安装Python包

使用 `conda install numpy`和 `pip install numpy`来安装Python包，虽然在表面上看起来非常相似，但实际上它们是为了不同的目的而设计的，因此存在一些关键的差异。

1. **包管理和环境管理**：

   - **Conda**：不仅是一个包管理器，也是一个环境管理器。它可以安装和管理来自Anaconda仓库以及Anaconda Cloud的conda包。Conda包是二进制包，这意味着安装它们时不需要编译器。此外，conda包不仅限于Python软件，还可以包含C或C++库、R包或任何其他软件。
   - **Pip**：是Python包管理工具，推荐用于从Python包索引（PyPI）安装包。Pip安装的是Python软件，打包为轮子（wheels）或源代码分发。后者可能需要在调用pip之前安装兼容的编译器和可能的库。
2. **环境隔离**：

   - **Conda**：具有创建隔离环境的能力，这些环境可以包含不同版本的Python和/或其中安装的包。这在处理数据科学工具时非常有用，因为不同的工具可能包含冲突的要求，这可能阻止它们全部安装在单一环境中。
   - **Pip**：没有内置支持环境，而是依赖于如virtualenv或venv等其他工具来创建隔离环境。工具如pipenv、poetry和hatch封装了pip和virtualenv，提供了一种统一的方法来处理这些环境。
3. **依赖关系管理**：

   - **Conda**：使用满足性（SAT）求解器来验证安装在环境中的所有包的所有要求都得到满足。这种检查可能需要额外的时间，但有助于防止创建损坏的环境。
   - **Pip**：在安装包时，以递归的序列循环安装依赖项。不会努力确保所有包的依赖项同时得到满足。这可能导致环境以微妙的方式损坏，如果按顺序先安装的包与后安装的包的依赖版本不兼容。
4. **包源**：

   - **Conda**：从Anaconda仓库和云安装包。
   - **Pip**：从Python包索引（PyPI）安装包。

总结来说，虽然 `conda`和 `pip`都可以用来安装Python包，但 `conda`提供了更广泛的功能，包括环境管理和跨语言包管理。`pip`则专注于Python包的安装，特别是当需要从源代码编译包时。在实践中，根据需要和可用的包，开发者可能会选择结合使用这两个工具。

### pip常用命令
```bash
# 安装包
pip install package_name

# 卸载包
pip uninstall package_name

# 列出已安装的包
pip list

# 检查可升级的包
pip list --outdated

# 升级包
pip install --upgrade package_name

# 查看包信息
pip show package_name

# 从requirements文件中安装所列的包
pip install -r requirements.txt

# 生成requirements文件,列出当前环境中所有已安装包
pip freeze > requirements.txt

# 安装指定版本的包
pip install package_name==version_number

#在PyPI上搜索包
pip search package_name

#列出pip的配置项
pip config list

#清理pip的缓存
pip cache purge

# 安装包时不下载任何依赖
pip install --no-deps package_name

# 使用特定源安装包
pip install package_name -i http://my.custom.repo/simple

# 安装编译依赖
pip install --no-binary :all:

# 限制包的安装位置
pip install package_name --target=/path/to/install
```
