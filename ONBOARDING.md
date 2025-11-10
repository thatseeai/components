# Onboarding Guide for New Developers

Welcome to the Angular Components team! This guide will help you get started as a new developer on the project. Whether you're a new team member or an external contributor, this document will walk you through everything you need to know to become productive quickly.

## Table of Contents

1. [Welcome to Angular Components](#welcome)
2. [Understanding the Project](#understanding-the-project)
3. [Development Environment Setup](#development-environment-setup)
4. [Codebase Structure](#codebase-structure)
5. [Your First Contribution](#your-first-contribution)
6. [Development Workflow](#development-workflow)
7. [Testing](#testing)
8. [Code Review Process](#code-review-process)
9. [Key Resources](#key-resources)
10. [Common Tasks](#common-tasks)
11. [Frequently Asked Questions](#faq)
12. [Getting Help](#getting-help)

---

## <a name="welcome"></a> 1. Welcome to Angular Components

Angular Components is the official UI component library for Angular applications. We maintain four primary packages:

- **@angular/cdk** - Component Development Kit: utilities for building custom components
- **@angular/material** - Material Design UI components for Angular
- **@angular/google-maps** - Angular wrapper for Google Maps JavaScript API
- **@angular/youtube-player** - Angular wrapper for YouTube Player API

### Our Goals

- Build high-quality, production-ready UI components
- Provide tools for developers to build custom components
- Ensure accessibility, internationalization, and performance
- Maintain comprehensive documentation and examples

### Team Values

- **Quality First**: All code is tested, documented, and reviewed
- **User-Centric**: We prioritize developer experience and accessibility
- **Collaboration**: We work together and help each other grow
- **Transparency**: Decisions and processes are open and documented

---

## <a name="understanding-the-project"></a> 2. Understanding the Project

### Tech Stack

- **Framework**: Angular 21.x
- **Language**: TypeScript 5.9.2 (strict mode)
- **Build System**: Bazel (Google's build tool)
- **Package Manager**: pnpm 10.20.0 (required)
- **Testing**: Jasmine + Karma
- **Styling**: Sass
- **Documentation**: Dgeni + custom Angular app

### Project Architecture

This is a **monorepo** containing 15 packages managed with pnpm workspaces:

```
@angular/cdk              - Core utilities
@angular/material         - Material Design components
@angular/google-maps      - Google Maps integration
@angular/youtube-player   - YouTube Player integration
@angular/aria             - ARIA accessibility utilities
+ experimental packages
+ date adapters (moment, luxon, date-fns)
```

### Browser and Accessibility Support

- **Browsers**: Last 2 versions of Chrome, Firefox, Safari, Edge
- **Screen Readers**: NVDA, JAWS, VoiceOver, TalkBack, ChromeVox

---

## <a name="development-environment-setup"></a> 3. Development Environment Setup

### Prerequisites

1. **Node.js**: Version 22.21.1 (see `.nvmrc`)
   ```bash
   # Install nvm if you haven't already
   curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash

   # Install and use the correct Node version
   nvm install
   nvm use
   ```

2. **pnpm**: Version 10.20.0 (required - npm/yarn are not supported)
   ```bash
   npm install -g pnpm@10.20.0
   ```

3. **Git**: Latest version recommended

### Initial Setup

1. **Fork and Clone**:
   ```bash
   # Fork the repository on GitHub first, then:
   git clone git@github.com:YOUR_USERNAME/components.git
   cd components

   # Add upstream remote
   git remote add upstream https://github.com/angular/components.git
   ```

2. **Install Dependencies**:
   ```bash
   pnpm install --frozen-lockfile
   ```
   This will take several minutes on first run.

3. **Verify Installation**:
   ```bash
   # Start the dev app to verify everything works
   pnpm dev-app
   ```
   Open http://localhost:4200 in your browser. You should see the component demo application.

### Windows Users

For Windows, you must use Windows Subsystem for Linux (WSL):

1. Run `wsl --install` from PowerShell (as administrator)
2. Restart your machine
3. Enter WSL with `wsl` command
4. Follow the setup steps as on Linux

See [DEV_ENVIRONMENT.md](DEV_ENVIRONMENT.md#windows) for more details.

---

## <a name="codebase-structure"></a> 4. Codebase Structure

### High-Level Directory Structure

```
components/
├── src/                      # Source code for all packages
│   ├── aria/                 # ARIA accessibility utilities
│   ├── cdk/                  # Component Development Kit (26 modules)
│   ├── material/             # Material Design components (41 components)
│   ├── google-maps/          # Google Maps wrapper
│   ├── youtube-player/       # YouTube Player wrapper
│   ├── dev-app/              # Development/demo application
│   ├── e2e-app/              # E2E testing app
│   ├── components-examples/  # Example code for documentation
│   └── universal-app/        # SSR testing app
│
├── docs/                     # Documentation site source
│   ├── src/                  # Angular app for docs
│   └── scenes/               # Component preview environment
│
├── tools/                    # Build and development tools
│   ├── bazel/                # Bazel build rules
│   ├── dgeni/                # Documentation generation
│   ├── tslint-rules/         # Custom lint rules
│   └── stylelint/            # Custom style lint rules
│
├── scripts/                  # Build and CI scripts
│   ├── build-packages-dist.mts      # Production build
│   ├── run-component-tests.mts      # Test runner
│   └── approve-api-golden.mts       # API approval tool
│
├── integration/              # Integration tests
├── guides/                   # Documentation guides
├── goldens/                  # API golden files
├── test/                     # Testing utilities
│
└── Configuration files:
    ├── package.json          # Root package configuration
    ├── pnpm-workspace.yaml   # Monorepo workspace config
    ├── tsconfig.json         # TypeScript config
    ├── .bazelrc              # Bazel configuration
    └── BUILD.bazel           # Build definitions
```

### Key Packages to Know

#### CDK (Component Development Kit)
Located in `src/cdk/`, provides utilities for building components:
- **a11y**: Accessibility utilities (focus management, live announcer)
- **overlay**: Positioning and overlay system
- **portal**: Dynamic component loading
- **drag-drop**: Drag and drop functionality
- **table**: Data table utilities
- **virtual-scroll**: Virtual scrolling for long lists
- And many more...

#### Material Components
Located in `src/material/`, includes 41+ Material Design components:
- Form controls: `button`, `checkbox`, `input`, `select`, `slider`
- Navigation: `menu`, `sidenav`, `tabs`, `toolbar`
- Layout: `card`, `expansion`, `grid-list`, `list`
- Data display: `table`, `paginator`, `sort`, `tree`
- And many more...

#### Development Apps

- **dev-app** (`src/dev-app/`): Comprehensive demo app with all components for manual testing
- **e2e-app** (`src/e2e-app/`): Simplified app for end-to-end tests
- **universal-app** (`src/universal-app/`): Tests server-side rendering (SSR)

---

## <a name="your-first-contribution"></a> 5. Your First Contribution

### Finding Your First Issue

1. **Good First Issues**: Look for issues labeled [`good first issue`](https://github.com/angular/components/issues?q=is%3Aissue+is%3Aopen+label%3A%22good+first+issue%22)
2. **Help Wanted**: Check [`help wanted`](https://github.com/angular/components/issues?q=is%3Aissue+is%3Aopen+label%3A%22help+wanted%22) for more opportunities
3. **Ask the Team**: Don't hesitate to ask in the issue comments if you'd like to work on something

### Before You Start

1. **Comment on the Issue**: Let others know you're working on it
2. **Understand the Scope**: Read the issue carefully and ask questions if unclear
3. **Check for Related Issues**: Search for similar or duplicate issues
4. **Sign the CLA**: You must sign the [Contributor License Agreement](https://code.google.com/legal/individual-cla-v1.0.html) before your first PR

### Making Your First Change

1. **Create a Branch**:
   ```bash
   git checkout -b my-fix-branch main
   ```

2. **Make Your Changes**:
   - Write code following our [Coding Standards](CODING_STANDARDS.md)
   - Add or update tests
   - Update documentation if needed

3. **Test Your Changes**:
   ```bash
   # Run unit tests
   pnpm test <component-name>

   # Run lint
   pnpm lint

   # Test in dev-app
   pnpm dev-app
   ```

4. **Commit Your Changes**:
   ```bash
   git add .
   git commit -m "fix(material/button): correct disabled state styling"
   ```
   Follow our [commit message guidelines](CONTRIBUTING.md#commit).

5. **Push and Create PR**:
   ```bash
   git push origin my-fix-branch
   ```
   Then create a Pull Request on GitHub targeting `components:main`.

---

## <a name="development-workflow"></a> 6. Development Workflow

### Daily Development Commands

```bash
# Start dev server with auto-reload
pnpm dev-app

# Run specific component tests
pnpm test button
pnpm test src/material/button    # Full path also works

# Run tests with debugging
pnpm test button --debug

# Run all linters
pnpm lint

# Run TypeScript lint only
pnpm tslint

# Run style lint only
pnpm stylelint

# Format code
pnpm format

# Build all packages for production
pnpm build

# Build and verify release output
pnpm build-and-check-release-output

# Run E2E tests
pnpm e2e

# Check circular dependencies
pnpm ts-circular-deps:check
```

### Working with the Dev App

The dev app (`pnpm dev-app`) is your primary development tool:

- **Location**: `src/dev-app/`
- **URL**: http://localhost:4200
- **Features**:
  - Live demos of all components
  - Interactive testing environment
  - Hot reload on code changes
  - Theme switcher (light/dark/custom)

**Tip**: Each component has a demo in `src/dev-app/<component-name>/`. Add your test cases there.

### Working with Documentation

```bash
# Start docs site locally
pnpm docs-app

# Build documentation content
pnpm build-docs-content
```

The documentation site is at http://localhost:4200 and includes:
- Component API documentation (auto-generated)
- Live examples with source code
- Guides and tutorials

---

## <a name="testing"></a> 7. Testing

### Unit Testing

We use **Jasmine** for unit tests and **Karma** as the test runner.

#### Running Tests

```bash
# Run tests for a specific component
pnpm test button

# Run tests for a specific path
pnpm test src/cdk/overlay

# Run with Firefox (default is Chrome)
pnpm test button --firefox

# Run locally (no remote browsers)
pnpm test button --local

# Debug tests (manual browser connection)
pnpm test button --debug
```

#### Writing Tests

Test files are located next to the source files with `.spec.ts` extension.

Example structure:
```typescript
describe('MatButton', () => {
  let fixture: ComponentFixture<TestComponent>;
  let button: MatButton;

  beforeEach(() => {
    TestBed.configureTestingModule({
      imports: [MatButtonModule],
      declarations: [TestComponent]
    });

    fixture = TestBed.createComponent(TestComponent);
    button = fixture.componentInstance.button;
    fixture.detectChanges();
  });

  it('should have correct disabled state', () => {
    expect(button.disabled).toBe(false);
    button.disabled = true;
    fixture.detectChanges();
    expect(button.disabled).toBe(true);
  });
});
```

**Key Testing Practices**:
- Test all public APIs
- Test user interactions
- Test accessibility features
- Use component harnesses when available
- Test error conditions and edge cases

### Component Harnesses

Component harnesses provide a robust API for testing components:

```typescript
import {MatButtonHarness} from '@angular/material/button/testing';

it('should click button using harness', async () => {
  const loader = TestbedHarnessEnvironment.loader(fixture);
  const button = await loader.getHarness(MatButtonHarness);
  await button.click();
  // Assert behavior...
});
```

See our [Component Harness Guide](guides/using-component-harnesses.md) for more details.

### E2E Testing

```bash
# Run all E2E tests
pnpm e2e

# Run specific E2E test
bazel test //src/material/button:e2e
```

E2E tests use Selenium WebDriver and are located in `src/e2e-app/`.

---

## <a name="code-review-process"></a> 8. Code Review Process

### What to Expect

1. **Initial Review**: A team member will review within a few days
2. **Feedback**: You may receive requests for changes
3. **Iteration**: Update your PR based on feedback
4. **Approval**: Once approved, a team member will merge
5. **CI Checks**: All automated tests must pass

### Review Checklist

Before requesting review, ensure:

- [ ] All tests pass (`pnpm test <component>`)
- [ ] Lint passes (`pnpm lint`)
- [ ] Code follows [Coding Standards](CODING_STANDARDS.md)
- [ ] Commit message follows [commit guidelines](CONTRIBUTING.md#commit)
- [ ] Documentation is updated if needed
- [ ] Public API changes are approved (`pnpm approve-api <target>`)
- [ ] Screenshots added for visual changes
- [ ] CLA is signed

### Responding to Feedback

```bash
# Make requested changes
# ... edit files ...

# Commit changes
git add .
git commit -m "address review feedback"

# Update PR
git push origin my-fix-branch
```

For detailed review guidelines, see [CODE_REVIEWS.md](CODE_REVIEWS.md).

---

## <a name="key-resources"></a> 9. Key Resources

### Documentation

- **Main Docs**: https://material.angular.dev
- **CDK Docs**: https://material.angular.dev/cdk/categories
- **API Reference**: Auto-generated from code comments
- **Guides**: See `/guides` directory

### Internal Documentation

- [README.md](README.md) - Project overview
- [CONTRIBUTING.md](CONTRIBUTING.md) - Contribution guidelines
- [DEV_ENVIRONMENT.md](DEV_ENVIRONMENT.md) - Environment setup
- [CODING_STANDARDS.md](CODING_STANDARDS.md) - Code standards
- [CODE_REVIEWS.md](CODE_REVIEWS.md) - Review process
- [FAQ.md](FAQ.md) - Frequently asked questions
- [SECURITY.md](SECURITY.md) - Security policies

### External Resources

- **Angular Docs**: https://angular.dev
- **Material Design**: https://material.io/design
- **TypeScript Handbook**: https://www.typescriptlang.org/docs/
- **Google TypeScript Style Guide**: https://google.github.io/styleguide/tsguide.html
- **Bazel Documentation**: https://bazel.build/

### Communication Channels

- **GitHub Issues**: Bug reports and feature requests
- **GitHub Discussions**: General questions and discussions
- **Stack Overflow**: Tag questions with `angular-material2`
- **Gitter**: https://gitter.im/angular/material2 (real-time chat)
- **Google Group**: https://groups.google.com/forum/#!forum/angular-material2

---

## <a name="common-tasks"></a> 10. Common Tasks

### Adding a New Component

1. **Create component structure** in `src/material/<component-name>/`
2. **Add to module**: Create module and public API
3. **Write tests**: Unit tests and harness tests
4. **Add to dev-app**: Create demo in `src/dev-app/<component-name>/`
5. **Add documentation**: API docs via comments, examples
6. **Add to build**: Update `BUILD.bazel` files
7. **Update golden files**: `pnpm approve-api material/<component-name>`

### Updating Public APIs

If you change a public API:

1. **Make your changes**
2. **Run approval tool**:
   ```bash
   pnpm approve-api <package>/<component>
   ```
3. **Review golden file changes** in `goldens/<package>/<component>.api.md`
4. **Commit golden files** with your changes

### Adding a Migration Schematic

Schematics help users update their code for breaking changes:

1. **Create schematic** in `src/material/schematics/ng-update/`
2. **Write migration logic**
3. **Add tests** in `src/material/schematics/ng-update/test-cases/`
4. **Update migration index**
5. **Document in CHANGELOG**

### Debugging Tips

```bash
# Debug dev-app in browser DevTools
pnpm dev-app
# Then open browser DevTools (F12)

# Debug unit tests
pnpm test <component> --debug
# Navigate to http://localhost:9876/debug.html

# Check Bazel build issues
bazel clean
pnpm install --frozen-lockfile

# Inspect Bazel cache
bazel info

# Run specific Bazel target
bazel test //src/material/button:unit_tests
```

### Working with Themes

Themes are in `src/material/core/theming/`:

```bash
# Test with different themes
# Use theme switcher in dev-app

# Generate custom theme
# See guides/theming.md

# Pre-built themes are in:
# src/material/prebuilt-themes/
```

---

## <a name="faq"></a> 11. Frequently Asked Questions

### General Questions

**Q: Why must I use pnpm?**
A: We use pnpm for its efficient disk usage, workspace support, and deterministic installs. npm and yarn are explicitly blocked.

**Q: Why Bazel?**
A: Bazel provides incremental builds, caching, and reproducibility. It's essential for a project of this size with many packages and dependencies.

**Q: Can I use Windows?**
A: Yes, but you must use WSL (Windows Subsystem for Linux). See [DEV_ENVIRONMENT.md](DEV_ENVIRONMENT.md#windows).

**Q: How long should CI take?**
A: Typical CI runs take 20-40 minutes. Failed checks will appear on your PR.

### Development Questions

**Q: Dev app won't start / build fails**
A: Try:
```bash
bazel clean
rm -rf node_modules pnpm-lock.yaml
pnpm install --frozen-lockfile
```

**Q: Tests pass locally but fail in CI**
A: Check for:
- Timing issues (use `fakeAsync` or `done()` callbacks)
- Browser-specific issues (CI tests on multiple browsers)
- Race conditions in async code

**Q: How do I test on different browsers?**
A: Use `pnpm test <target> --firefox` or configure Karma for other browsers.

**Q: My commit message was rejected**
A: Ensure you follow the [commit message format](CONTRIBUTING.md#commit):
```
<type>(<package>/<scope>): <subject>
```
Example: `fix(material/button): resolve disabled state issue`

### Code Questions

**Q: Where do I add my test?**
A: Next to the source file with `.spec.ts` extension.

**Q: What's the difference between CDK and Material?**
A: CDK provides behavior and utilities; Material provides styled components following Material Design.

**Q: How do I make a component accessible?**
A: Use CDK accessibility utilities (`a11y` module), proper ARIA attributes, keyboard navigation, and test with screen readers.

**Q: Should I update documentation?**
A: Yes, if you change public APIs or add features. Update API docs via code comments and add examples if needed.

### Process Questions

**Q: How long until my PR is reviewed?**
A: Typically within a few days, but can vary based on team availability and PR complexity.

**Q: Can I work on multiple issues?**
A: Yes, but consider starting with one to familiarize yourself with the workflow.

**Q: My PR was closed, why?**
A: Common reasons:
- No CLA signed
- Doesn't follow guidelines
- Duplicate of another PR
- Issue was decided against

**Q: How do I get my PR reopened?**
A: Address the closure reason and comment on the PR explaining your updates.

---

## <a name="getting-help"></a> 12. Getting Help

### When You're Stuck

1. **Search Existing Issues**: Your question may already be answered
2. **Check Documentation**: Review guides and API docs
3. **Ask in Issue Comments**: If working on an issue, ask there
4. **Stack Overflow**: Tag questions with `angular-material2`
5. **Gitter Chat**: For quick questions: https://gitter.im/angular/material2

### Reporting Problems

**For Bugs**:
1. Create a minimal reproduction (StackBlitz, CodePen, etc.)
2. Include Angular and Material versions
3. Describe expected vs. actual behavior
4. Add screenshots for visual issues

**For Build/Setup Issues**:
1. Share error messages (full output)
2. List your environment (OS, Node version, pnpm version)
3. Describe steps to reproduce

### Learning Resources

**New to Angular?**
- [Angular Tutorial](https://angular.dev/tutorials)
- [Angular Documentation](https://angular.dev/overview)

**New to TypeScript?**
- [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html)
- [TypeScript Deep Dive](https://basarat.gitbook.io/typescript/)

**New to Material Design?**
- [Material Design Guidelines](https://material.io/design)
- [Material Design Components](https://material.io/components)

**New to Accessibility?**
- [Web Accessibility Initiative (WAI)](https://www.w3.org/WAI/)
- [ARIA Authoring Practices](https://www.w3.org/WAI/ARIA/apg/)

---

## Welcome Aboard!

You're now ready to start contributing to Angular Components! Remember:

- **Start Small**: Begin with good first issues
- **Ask Questions**: The team is here to help
- **Be Patient**: Learning a large codebase takes time
- **Have Fun**: Building great UI components is rewarding!

We're excited to have you on the team. Happy coding!

---

## Quick Reference

```bash
# Essential Commands
pnpm install              # Install dependencies
pnpm dev-app             # Start dev server
pnpm test <target>       # Run tests
pnpm lint                # Run linters
pnpm format              # Format code
pnpm build               # Build packages

# Common Tasks
pnpm approve-api <pkg>   # Approve API changes
pnpm breaking-changes    # Check breaking changes
pnpm e2e                 # Run E2E tests

# Useful Links
GitHub: https://github.com/angular/components
Docs: https://material.angular.dev
Issues: https://github.com/angular/components/issues
Chat: https://gitter.im/angular/material2
```

For more detailed information, refer to the individual documentation files linked throughout this guide.
