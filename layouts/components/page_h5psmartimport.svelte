<script>
  export let title, examples, bestPractices, promptTemplates, contentTypes, interactiveBookContents;

  // Set defaults for safety
  examples = examples || [];
  bestPractices = bestPractices || { worksWell: [], doesntWork: [] };
  promptTemplates = promptTemplates || [];
  contentTypes = contentTypes || [];
  interactiveBookContents = interactiveBookContents || [];

  let activeTab = 'no-custom';
  let contentTypesTab = 'all-types';

  $: activeExample = examples.find(ex => ex.id === activeTab);
</script>

<div class="container">
  <div class="max-w">
    <!-- Header -->
    <div class="header">
      <div class="header-content">
        <svg class="sparkles-icon" width="40" height="40" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <path d="m12 3-1.912 5.813a2 2 0 0 1-1.275 1.275L3 12l5.813 1.912a2 2 0 0 1 1.275 1.275L12 21l1.912-5.813a2 2 0 0 1 1.275-1.275L21 12l-5.813-1.912a2 2 0 0 1-1.275-1.275L12 3Z"/>
          <path d="M5 3v4"/>
          <path d="M19 17v4"/>
          <path d="M3 5h4"/>
          <path d="M17 19h4"/>
        </svg>
        <h1 class="main-title">{title}</h1>
      </div>
      <p class="subtitle">
        Empower content creators with in-depth customization options to generate H5P activities aligned to students' skills and learning objectives
      </p>
    </div>

    <!-- Content Types Section -->
    {#if contentTypes && contentTypes.length > 0}
    <div class="content-types-section">
      <!-- Section Header -->
      <div class="templates-section" style="margin-bottom: 2rem;">
        <div class="templates-header">
          <div class="templates-icon-container" style="background: linear-gradient(to bottom right, #93c5fd, #60a5fa);">
            <svg width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <rect x="3" y="3" width="18" height="18" rx="2" ry="2"/>
              <line x1="3" y1="9" x2="21" y2="9"/>
              <line x1="9" y1="21" x2="9" y2="9"/>
            </svg>
          </div>
          <div>
            <h3 class="templates-title">Content Types Supported by Smart Import</h3>
            <p class="templates-description">Smart Import can generate multiple H5P content types, each optimized for different learning objectives</p>
          </div>
        </div>
      </div>

      <!-- Content Types Tab Navigation -->
      <div class="tab-navigation">
        <div class="tab-buttons">
          <button
            on:click={() => contentTypesTab = 'all-types'}
            class="tab-button"
            class:active={contentTypesTab === 'all-types'}
            style={contentTypesTab === 'all-types' ? 'background: linear-gradient(to right, #93c5fd, #60a5fa);' : ''}
          >
            <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <rect x="3" y="3" width="18" height="18" rx="2" ry="2"/>
              <line x1="3" y1="9" x2="21" y2="9"/>
              <line x1="9" y1="21" x2="9" y2="9"/>
            </svg>
            <span class="tab-text">All Content Types</span>
          </button>
          <button
            on:click={() => contentTypesTab = 'interactive-book'}
            class="tab-button"
            class:active={contentTypesTab === 'interactive-book'}
            style={contentTypesTab === 'interactive-book' ? 'background: linear-gradient(to right, #d8b4fe, #c084fc);' : ''}
          >
            <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <path d="M4 19.5v-15A2.5 2.5 0 0 1 6.5 2H20v20H6.5a2.5 2.5 0 0 1 0-5H20"/>
            </svg>
            <span class="tab-text">Interactive Book</span>
          </button>
        </div>
      </div>

      <!-- All Content Types Tab -->
      {#if contentTypesTab === 'all-types'}
        <div class="ct-content-grid">
          {#each contentTypes as contentType}
            <div class="ct-content-card">
              <div class="ct-card-layout">
                <div class="ct-icon-container">
                  <img
                    src={contentType.icon}
                    alt={`${contentType.name} icon`}
                    class="ct-content-icon"
                  />
                </div>
                <div class="ct-card-content">
                  <div style="display: flex; align-items: center; gap: 0.5rem; margin-bottom: 0.25rem;">
                    <h3 class="ct-content-name" style="margin-bottom: 0;">{contentType.name}</h3>
                    {#if contentType.flag}
                      <span class="ct-new-flag">{contentType.flag}</span>
                    {/if}
                  </div>
                  <div class="ct-badge-container">
                    <span class="ct-badge blue-badge">{contentType.contentType}</span>
                  </div>
                  <p class="ct-content-description">{contentType.description}</p>
                </div>
              </div>
            </div>
          {/each}
        </div>
      {/if}

      <!-- Interactive Book Tab -->
      {#if contentTypesTab === 'interactive-book'}
        <div class="ct-info-box purple-info">
          <p class="ct-info-text">
            <strong class="ct-info-strong">Note:</strong> An Interactive Book is a comprehensive learning resource that combines multiple content types into a single, cohesive learning experience. All components below are generated automatically within one Interactive Book activity.
          </p>
        </div>

        <div class="ct-content-grid">
          {#each interactiveBookContents as content}
            <div class="ct-content-card purple-hover">
              <div class="ct-card-layout">
                {#if content.icon.startsWith('media/')}
                  <div class="ct-icon-container">
                    <img
                      src={content.icon}
                      alt={`${content.name} icon`}
                      class="ct-content-icon"
                    />
                  </div>
                {:else}
                  <div class="ct-emoji-icon">{content.icon}</div>
                {/if}
                <div class="ct-card-content">
                  <h3 class="ct-content-name">{content.name}</h3>
                  <div class="ct-badge-container">
                    <span class="ct-badge purple-badge">{content.type}</span>
                  </div>
                  <p class="ct-content-description">{content.description}</p>
                </div>
              </div>
            </div>
          {/each}
        </div>
      {/if}
    </div>
    {/if}

    <!-- Customization Examples Section Header -->
    <div class="customization-header">
      <h2 class="section-title">Prompt Customization Examples</h2>
      <p class="section-subtitle">See how different prompts create tailored learning experiences</p>
    </div>

    <!-- Tab Navigation -->
    {#if examples && examples.length > 0}
    <div class="tab-navigation">
      <div class="tab-buttons">
        {#each examples as example, idx}
          <button
            on:click={() => activeTab = example.id}
            class="tab-button"
            class:active={activeTab === example.id}
            style={activeTab === example.id ? `background: linear-gradient(to right, ${example.colorFrom}, ${example.colorTo});` : ''}
          >
            {#if example.id === 'no-custom'}
              <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                <path d="m12 3-1.912 5.813a2 2 0 0 1-1.275 1.275L3 12l5.813 1.912a2 2 0 0 1 1.275 1.275L12 21l1.912-5.813a2 2 0 0 1 1.275-1.275L21 12l-5.813-1.912a2 2 0 0 1-1.275-1.275L12 3Z"/>
              </svg>
            {:else if example.id === 'user-groups'}
              <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                <path d="M16 21v-2a4 4 0 0 0-4-4H6a4 4 0 0 0-4 4v2"/>
                <circle cx="9" cy="7" r="4"/>
                <path d="M22 21v-2a4 4 0 0 0-3-3.87"/>
                <path d="M16 3.13a4 4 0 0 1 0 7.75"/>
              </svg>
            {:else if example.id === 'user-output'}
              <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                <circle cx="12" cy="12" r="10"/>
                <circle cx="12" cy="12" r="6"/>
                <circle cx="12" cy="12" r="2"/>
              </svg>
            {:else}
              <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                <path d="M4 19.5v-15A2.5 2.5 0 0 1 6.5 2H20v20H6.5a2.5 2.5 0 0 1 0-5H20"/>
              </svg>
            {/if}
            <span class="tab-text">{example.title.split(' ')[0]}</span>
            <span class="tab-text-mobile">Ex {idx + 1}</span>
          </button>
        {/each}
      </div>
    </div>
    {/if}

    <!-- Main Content Area -->
    <div class="main-content">
      {#if activeExample}
        <div class="example-card" style="border-left-color: {activeExample.borderColor};">
          <div class="card-header">
            <div class="icon-container" style="background: linear-gradient(to bottom right, {activeExample.colorFrom}, {activeExample.colorTo});">
              {#if activeExample.id === 'no-custom'}
                <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                  <path d="m12 3-1.912 5.813a2 2 0 0 1-1.275 1.275L3 12l5.813 1.912a2 2 0 0 1 1.275 1.275L12 21l1.912-5.813a2 2 0 0 1 1.275-1.275L21 12l-5.813-1.912a2 2 0 0 1-1.275-1.275L12 3Z"/>
                </svg>
              {:else if activeExample.id === 'user-groups'}
                <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                  <path d="M16 21v-2a4 4 0 0 0-4-4H6a4 4 0 0 0-4 4v2"/>
                  <circle cx="9" cy="7" r="4"/>
                  <path d="M22 21v-2a4 4 0 0 0-3-3.87"/>
                  <path d="M16 3.13a4 4 0 0 1 0 7.75"/>
                </svg>
              {:else if activeExample.id === 'user-output'}
                <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                  <circle cx="12" cy="12" r="10"/>
                  <circle cx="12" cy="12" r="6"/>
                  <circle cx="12" cy="12" r="2"/>
                </svg>
              {:else}
                <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                  <path d="M4 19.5v-15A2.5 2.5 0 0 1 6.5 2H20v20H6.5a2.5 2.5 0 0 1 0-5H20"/>
                </svg>
              {/if}
            </div>
            <div>
              <h2 class="card-title">{activeExample.title}</h2>
              <p class="card-description">{activeExample.description}</p>
            </div>
          </div>

          <div class="detail-box" style="background-color: {activeExample.bgColor}; border-color: {activeExample.borderColor};">
            <p class="detail-text">{activeExample.details}</p>
          </div>

          <!-- Prompt Section -->
          <div class="prompt-section">
            <div class="prompt-header">
              <svg class="lightbulb-icon" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                <path d="M15 14c.2-1 .7-1.7 1.5-2.5 1-.9 1.5-2.2 1.5-3.5A6 6 0 0 0 6 8c0 1 .2 2.2 1.5 3.5.7.7 1.3 1.5 1.5 2.5"/>
                <path d="M9 18h6"/>
                <path d="M10 22h4"/>
              </svg>
              <h3 class="prompt-title">Example Prompt</h3>
            </div>
            <div class="prompt-box" style="border-left-color: {activeExample.borderColor};">
              <p class="prompt-text">"{activeExample.prompt}"</p>
              <div class="prompt-tags">
                <span class="tag tag-colored" style="background: linear-gradient(to right, {activeExample.colorFrom}, {activeExample.colorTo});">{activeExample.promptType}</span>
                <span class="tag tag-gray">{activeExample.output}</span>
              </div>
            </div>
          </div>

          <!-- Key Concepts Output -->
          <div class="concepts-section">
            <h3 class="concepts-title">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="color: {activeExample.accentColor};">
                <path d="M5 12h14"/>
                <path d="m12 5 7 7-7 7"/>
              </svg>
              Generated Key Concepts
            </h3>
            <div class="concepts-grid">
              {#each activeExample.example as concept}
                <div class="concept-card" style="--hover-border-color: {activeExample.hoverBorder};">
                  {concept}
                </div>
              {/each}
            </div>
          </div>
        </div>
      {/if}
    </div>

    <!-- Best Practices Section -->
    <div class="best-practices">
      <!-- What Works Best -->
      <div class="practice-card works-best">
        <div class="practice-header">
          <div class="practice-icon-container green">
            <svg width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <path d="M22 11.08V12a10 10 0 1 1-5.93-9.14"/>
              <polyline points="22 4 12 14.01 9 11.01"/>
            </svg>
          </div>
          <h3 class="practice-title">What Works Best</h3>
        </div>
        <div class="practice-items">
          {#each bestPractices.worksWell as practice}
          <div class="practice-item green">
            <h4 class="practice-item-title green">✓ {practice.title}</h4>
            <p class="practice-item-text">{practice.text}</p>
          </div>
          {/each}
        </div>
      </div>

      <!-- What Doesn't Work -->
      <div class="practice-card doesnt-work">
        <div class="practice-header">
          <div class="practice-icon-container red">
            <svg width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <circle cx="12" cy="12" r="10"/>
              <line x1="12" y1="8" x2="12" y2="12"/>
              <line x1="12" y1="16" x2="12.01" y2="16"/>
            </svg>
          </div>
          <h3 class="practice-title">What Doesn't Work As Expected</h3>
        </div>
        <div class="practice-items">
          {#each bestPractices.doesntWork as practice}
          <div class="practice-item red">
            <h4 class="practice-item-title red">✗ {practice.title}</h4>
            <p class="practice-item-text">{practice.text}</p>
          </div>
          {/each}
        </div>
      </div>
    </div>

    <!-- Prompt Templates -->
    <div class="templates-section">
      <div class="templates-header">
        <div class="templates-icon-container">
          <svg width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M15 14c.2-1 .7-1.7 1.5-2.5 1-.9 1.5-2.2 1.5-3.5A6 6 0 0 0 6 8c0 1 .2 2.2 1.5 3.5.7.7 1.3 1.5 1.5 2.5"/>
            <path d="M9 18h6"/>
            <path d="M10 22h4"/>
          </svg>
        </div>
        <h3 class="templates-title">Prompt Templates</h3>
      </div>
      <p class="templates-description">Use prompts like these to get the most out of Smart Import:</p>
      <div class="templates-grid">
        {#each promptTemplates as template}
        <div class="template-card">
          <div class="template-text">{template}</div>
        </div>
        {/each}
      </div>
    </div>
  </div>
</div>

<style>
  /* Container & Layout */
  .container {
    min-height: 100vh;
    background-color: var(--background);
    color: var(--on-background);
    padding: 2rem;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Roboto', 'Oxygen', 'Ubuntu', 'Cantarell', 'Fira Sans', 'Droid Sans', 'Helvetica Neue', sans-serif;
    /* Full width breakout */
    width: 100vw;
    position: relative;
    left: 50%;
    transform: translateX(-50%);
    margin-top: -3rem;
    margin-bottom: -3rem;
  }

  .max-w {
    max-width: 80rem;
    margin: 0 auto;
  }

  /* Header */
  .header {
    margin-bottom: 3rem;
    text-align: center;
  }

  .header-content {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 0.75rem;
    margin-bottom: 1rem;
  }

  .sparkles-icon {
    color: var(--accent);
  }

  .main-title {
    font-size: 3rem;
    font-weight: bold;
    color: var(--on-background);
  }

  .subtitle {
    font-size: 1.25rem;
    color: var(--on-background);
    opacity: 0.8;
    max-width: 48rem;
    margin: 0 auto;
  }

  /* Tab Navigation */
  .tab-navigation {
    margin-bottom: 2rem;
    background-color: var(--surface);
    border-radius: 0.5rem;
    padding: 0.5rem;
    backdrop-filter: blur(8px);
    border: 1px solid rgba(255, 255, 255, 0.1);
    overflow-x: auto;
  }

  .tab-buttons {
    display: flex;
    gap: 0.5rem;
    min-width: 100%;
  }

  .tab-button {
    padding: 0.75rem 1rem;
    border-radius: 0.5rem;
    font-weight: 600;
    transition: all 0.3s ease;
    white-space: nowrap;
    display: flex;
    align-items: center;
    gap: 0.5rem;
    border: none;
    cursor: pointer;
    background-color: rgba(255, 255, 255, 0.1);
    color: var(--on-surface);
  }

  .tab-button:hover {
    background-color: rgba(255, 255, 255, 0.15);
  }

  .tab-button.active {
    box-shadow: 0 10px 15px -3px rgba(59, 130, 246, 0.5);
    color: #1e293b;
  }

  .tab-text-mobile {
    display: none;
  }

  @media (max-width: 640px) {
    .tab-text {
      display: none;
    }
    .tab-text-mobile {
      display: inline;
    }
    .main-title {
      font-size: 2rem;
    }
  }

  /* Main Content */
  .main-content {
    margin-bottom: 3rem;
  }

  .example-card {
    background-color: white;
    padding: 2rem;
    border-radius: 0.75rem;
    box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
    border-left: 8px solid;
  }

  .card-header {
    display: flex;
    align-items: flex-start;
    gap: 1rem;
    margin-bottom: 1.5rem;
  }

  .icon-container {
    padding: 0.75rem;
    border-radius: 0.5rem;
    color: white;
    box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
  }

  .icon-container svg {
    width: 24px;
    height: 24px;
  }

  .card-title {
    font-size: 1.875rem;
    font-weight: bold;
    margin-bottom: 0.5rem;
    color: #1e293b;
  }

  .card-description {
    color: #334155;
    font-size: 1.125rem;
  }

  .detail-box {
    border-radius: 0.5rem;
    padding: 1.5rem;
    margin-bottom: 1.5rem;
    border: 1px solid;
    opacity: 0.9;
  }

  .detail-text {
    color: #334155;
  }

  /* Prompt Section */
  .prompt-section {
    margin-bottom: 1.5rem;
  }

  .prompt-header {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    margin-bottom: 0.75rem;
  }

  .lightbulb-icon {
    color: #d97706;
  }

  .prompt-title {
    font-size: 1.125rem;
    font-weight: 600;
    color: #1e293b;
  }

  .prompt-box {
    background-color: #f8fafc;
    border-radius: 0.5rem;
    padding: 1rem;
    border-left: 4px solid;
  }

  .prompt-text {
    font-size: 1.125rem;
    font-style: italic;
    color: #1e293b;
    margin-bottom: 0.75rem;
  }

  .prompt-tags {
    margin-top: 0.75rem;
    padding-top: 0.75rem;
    border-top: 1px solid #e2e8f0;
    display: flex;
    flex-wrap: wrap;
    gap: 0.75rem;
  }

  .tag {
    font-size: 0.875rem;
    padding: 0.25rem 0.75rem;
    border-radius: 9999px;
    font-weight: 500;
  }

  .tag-colored {
    color: white;
  }

  .tag-gray {
    background-color: #e2e8f0;
    color: #334155;
  }

  /* Key Concepts */
  .concepts-section {
    margin-bottom: 1rem;
  }

  .concepts-title {
    font-size: 1.125rem;
    font-weight: 600;
    margin-bottom: 0.75rem;
    display: flex;
    align-items: center;
    gap: 0.5rem;
    color: #1e293b;
  }

  .concepts-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 0.75rem;
  }

  @media (min-width: 768px) {
    .concepts-grid {
      grid-template-columns: repeat(3, 1fr);
    }
  }

  .concept-card {
    background-color: #f8fafc;
    border-radius: 0.5rem;
    padding: 0.75rem;
    text-align: center;
    font-size: 0.875rem;
    border: 2px solid #e2e8f0;
    transition: all 0.3s ease;
    color: #1e293b;
    font-weight: 500;
  }

  .concept-card:hover {
    border-color: var(--hover-border-color);
  }

  /* Best Practices */
  .best-practices {
    display: grid;
    grid-template-columns: 1fr;
    gap: 2rem;
    margin-bottom: 3rem;
  }

  @media (min-width: 768px) {
    .best-practices {
      grid-template-columns: repeat(2, 1fr);
    }
  }

  .practice-card {
    background-color: white;
    border-radius: 0.75rem;
    padding: 2rem;
    box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
  }

  .works-best {
    border-left: 8px solid #4ade80;
  }

  .doesnt-work {
    border-left: 8px solid #fb923c;
  }

  .practice-header {
    display: flex;
    align-items: center;
    gap: 0.75rem;
    margin-bottom: 1.5rem;
  }

  .practice-icon-container {
    padding: 0.75rem;
    border-radius: 0.5rem;
    color: white;
    box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
  }

  .practice-icon-container.green {
    background: linear-gradient(to bottom right, #86efac, #4ade80);
  }

  .practice-icon-container.red {
    background: linear-gradient(to bottom right, #fca5a5, #fb923c);
  }

  .practice-title {
    font-size: 1.5rem;
    font-weight: bold;
    color: #1e293b;
  }

  .practice-items {
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }

  .practice-item {
    border-radius: 0.5rem;
    padding: 1rem;
    border-left: 4px solid;
  }

  .practice-item.green {
    background-color: #f0fdf4;
    border-color: #4ade80;
  }

  .practice-item.red {
    background-color: #fff7ed;
    border-color: #fb923c;
  }

  .practice-item-title {
    font-weight: 600;
    margin-bottom: 0.5rem;
  }

  .practice-item-title.green {
    color: #15803d;
  }

  .practice-item-title.red {
    color: #c2410c;
  }

  .practice-item-text {
    color: #334155;
  }

  /* Prompt Templates */
  .templates-section {
    background-color: white;
    border-radius: 0.75rem;
    padding: 2rem;
    border-left: 8px solid #818cf8;
    box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
  }

  .templates-header {
    display: flex;
    align-items: center;
    gap: 0.75rem;
    margin-bottom: 1.5rem;
  }

  .templates-icon-container {
    background: linear-gradient(to bottom right, #a5b4fc, #818cf8);
    padding: 0.75rem;
    border-radius: 0.5rem;
    color: white;
    box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
  }

  .templates-title {
    font-size: 1.5rem;
    font-weight: bold;
    color: #1e293b;
  }

  .templates-description {
    color: #334155;
    margin-bottom: 1.5rem;
  }

  .templates-grid {
    display: grid;
    grid-template-columns: 1fr;
    gap: 1rem;
  }

  @media (min-width: 768px) {
    .templates-grid {
      grid-template-columns: repeat(3, 1fr);
    }
  }

  .template-card {
    background-color: #eef2ff;
    border-radius: 0.5rem;
    padding: 1rem;
    border: 2px solid #c7d2fe;
    transition: all 0.3s ease;
  }

  .template-card:hover {
    border-color: #818cf8;
  }

  .template-text {
    color: #3730a3;
    font-family: monospace;
    font-size: 0.875rem;
    font-weight: 500;
    text-align: center;
  }

  /* Content Types Section */
  .content-types-section {
    margin-bottom: 4rem;
  }

  .ct-section-header {
    background-color: white;
    border-radius: 0.75rem;
    padding: 2rem;
    box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
    margin-bottom: 2rem;
    border-left: 8px solid #60a5fa;
    display: flex;
    align-items: center;
    gap: 1rem;
  }

  .ct-header-icon {
    padding: 0.75rem;
    border-radius: 0.5rem;
    color: white;
    box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
    flex-shrink: 0;
  }

  .blue-gradient {
    background: linear-gradient(to bottom right, #93c5fd, #60a5fa);
  }

  .ct-section-title {
    font-size: 1.875rem;
    font-weight: bold;
    color: #1e293b;
    margin-bottom: 0.25rem;
  }

  .ct-section-description {
    color: #64748b;
  }

  /* Content Types Tab Navigation */
  .ct-tab-navigation {
    margin-bottom: 2rem;
    background-color: var(--surface);
    border-radius: 0.5rem;
    padding: 0.5rem;
    backdrop-filter: blur(8px);
    border: 1px solid rgba(255, 255, 255, 0.1);
  }

  .ct-tab-buttons {
    display: flex;
    gap: 0.5rem;
  }

  .ct-tab-button {
    flex: 1;
    padding: 0.75rem 1.5rem;
    border-radius: 0.5rem;
    font-weight: 600;
    transition: all 0.3s ease;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 0.5rem;
    border: none;
    cursor: pointer;
    background-color: rgba(255, 255, 255, 0.1);
    color: var(--on-surface);
  }

  .ct-tab-button:hover {
    background-color: rgba(255, 255, 255, 0.15);
  }

  .ct-tab-button.active {
    box-shadow: 0 10px 15px -3px rgba(59, 130, 246, 0.5);
    color: #1e293b;
  }

  /* Content Types Grid */
  .ct-content-grid {
    display: grid;
    grid-template-columns: 1fr;
    gap: 1.5rem;
  }

  @media (min-width: 768px) {
    .ct-content-grid {
      grid-template-columns: repeat(2, 1fr);
    }
  }

  .ct-content-card {
    background-color: white;
    border-radius: 0.5rem;
    padding: 1.5rem;
    border-left: 4px solid #e2e8f0;
    transition: all 0.3s ease;
    box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
  }

  .ct-content-card:hover {
    border-left-color: #60a5fa;
    box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1);
  }

  .ct-content-card.purple-hover:hover {
    border-left-color: #c084fc;
  }

  .ct-card-layout {
    display: flex;
    align-items: flex-start;
    gap: 1rem;
  }

  .ct-icon-container {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 4rem;
    width: 4rem;
    flex-shrink: 0;
  }

  .ct-content-icon {
    max-height: 4rem;
    max-width: 4rem;
    object-fit: contain;
    transition: transform 0.3s ease;
  }

  .ct-content-card:hover .ct-content-icon {
    transform: scale(1.1);
  }

  .ct-emoji-icon {
    font-size: 2.5rem;
    flex-shrink: 0;
  }

  .ct-card-content {
    flex: 1;
  }

  .ct-content-name {
    font-size: 1.25rem;
    font-weight: bold;
    color: #1e293b;
    margin-bottom: 0.25rem;
  }

  .ct-badge-container {
    margin-bottom: 0.5rem;
  }

  .ct-badge {
    font-size: 0.75rem;
    padding: 0.25rem 0.75rem;
    border-radius: 9999px;
    font-weight: 500;
    display: inline-block;
  }

  .blue-badge {
    background-color: #dbeafe;
    color: #1e40af;
  }

  .purple-badge {
    background-color: #f3e8ff;
    color: #6b21a8;
  }

  .ct-content-description {
    font-size: 0.875rem;
    color: #64748b;
  }

  .ct-new-flag {
    font-size: 0.75rem;
    padding: 0.125rem 0.5rem;
    border-radius: 9999px;
    font-weight: 600;
    background: linear-gradient(to right, #34d399, #10b981);
    color: white;
    text-transform: uppercase;
    letter-spacing: 0.025em;
  }

  /* Info Box */
  .ct-info-box {
    border-radius: 0.5rem;
    padding: 1.5rem;
    border-left: 4px solid;
    margin-bottom: 2rem;
  }

  .purple-info {
    background-color: #faf5ff;
    border-left-color: #c084fc;
  }

  .ct-info-text {
    color: #334155;
  }

  .ct-info-strong {
    color: #6b21a8;
  }

  /* Customization Header */
  .customization-header {
    text-align: center;
    margin-bottom: 2rem;
  }

  .section-title {
    font-size: 2rem;
    font-weight: bold;
    color: var(--on-background);
    margin-bottom: 0.5rem;
  }

  .section-subtitle {
    font-size: 1.125rem;
    color: var(--on-background);
    opacity: 0.8;
  }

  /* Mobile Responsive for Content Types */
  @media (max-width: 640px) {
    .ct-section-header {
      flex-direction: column;
      text-align: center;
    }

    .ct-tab-buttons {
      flex-direction: column;
    }
  }
</style>
