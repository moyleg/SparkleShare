# SparkleShare Build Guide

This document explains how to build SparkleShare and create releases using the automated GitHub Actions workflows.

## 🚀 Quick Start

### Automatic Builds

The project now includes automated build workflows that run on GitHub Actions:

1. **Push to any branch** → Triggers Windows build
2. **Create a git tag** → Triggers full release build with packages

### Manual Local Build

If you want to build locally on Windows:

```powershell
# 1. Restore NuGet packages
nuget restore SparkleShare.sln

# 2. Build the solution
msbuild SparkleShare.sln /p:Configuration=Release /p:Platform="Any CPU"
```

## 📦 Creating Releases

### Using GitHub Actions (Recommended)

1. **Commit and push your changes:**
   ```bash
   git add .
   git commit -m "Release version 1.5.0"
   git push origin main
   ```

2. **Create and push a tag:**
   ```bash
   git tag v1.5.0
   git push origin v1.5.0
   ```

3. **Wait for the build:**
   - Go to GitHub Actions tab
   - Watch the "Create Release" workflow
   - Download artifacts when complete

### What Gets Built

The automated build creates:
- ✅ **Windows executable** (SparkleShare.Windows.exe)
- ✅ **All dependencies** (DLLs, images, presets)
- ✅ **Launcher script** (Launch-SparkleShare.bat)
- ✅ **Installation guide** (README.md)
- ✅ **ZIP package** ready for distribution

## 🔧 Build Workflows

### 1. build-windows.yml
- **Triggers:** Push to any branch, Pull Requests
- **Purpose:** Continuous integration builds
- **Output:** Build artifacts for testing

### 2. release.yml  
- **Triggers:** Git tags (v*)
- **Purpose:** Create official releases
- **Output:** GitHub release with downloadable ZIP

### 3. build-and-release.yml
- **Triggers:** Tags, main/develop branches
- **Purpose:** Multi-platform builds (Windows + Linux)
- **Output:** Multiple platform packages

## 🐛 Bug Fixes Applied

This build includes all the critical fixes we applied:

1. **Thread Safety** - Replaced `Thread.Abort()` with cancellation tokens
2. **Memory Leaks** - Fixed crypto object disposal
3. **SSH Connectivity** - Dynamic port handling  
4. **File Operations** - Corrected file existence checks
5. **Resource Management** - Proper disposal patterns
6. **Git Configuration** - Safer config handling
7. **Process Stability** - Eliminated `Environment.Exit()`
8. **Input Validation** - Added comprehensive validation

## 🏃‍♂️ Testing the Build

After a successful build:

1. **Download** the ZIP from GitHub Releases
2. **Extract** to a folder (e.g., `C:\SparkleShare\`)
3. **Run** `Launch-SparkleShare.bat`
4. **Verify** the application starts without crashes
5. **Test** basic functionality (add repository, sync files)

## 🔍 Troubleshooting Builds

### Build Fails - Missing Dependencies
- Check that NuGet packages restore correctly
- Verify .NET Framework 4.8 is available
- Ensure all image files are present

### Build Succeeds But App Crashes
- Check Windows Event Viewer for .NET runtime errors
- Verify Git is available in system PATH
- Test with a simple Git repository first

### Linux Build Issues  
- Mono version compatibility
- GTK dependencies
- Package manager differences

## 📋 Release Checklist

Before creating a release:

- [ ] All tests pass locally
- [ ] Bug fixes are verified
- [ ] Version number updated
- [ ] Release notes prepared
- [ ] Git tag follows semantic versioning (v1.2.3)

## 🤝 Contributing

To contribute to the build process:

1. Fork the repository
2. Create a feature branch
3. Test your changes with GitHub Actions
4. Submit a pull request

The build workflows will automatically test your changes!

## 📚 Additional Resources

- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [MSBuild Reference](https://docs.microsoft.com/en-us/visualstudio/msbuild/)
- [NuGet Package Manager](https://docs.microsoft.com/en-us/nuget/)
- [SparkleShare Wiki](https://github.com/hbons/SparkleShare/wiki)

---

**Happy building!** 🎉