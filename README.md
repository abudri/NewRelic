# New Relic

Notes for New Relic work.

## How to Install New Relic Ruby Agent

### Steps

1. Have a Ruby application ready for which you want the APM. For me I found from a site the repo for the Rails Tutorial, in this case from JetBrains, which is just a fork of the project:

[https://github.com/JetBrains/sample_rails_app](https://github.com/JetBrains/sample_rails_app)

2. Then I went to New Relic One APM section, and hit Get Started in lower right:

<img src="https://user-images.githubusercontent.com/17362519/113585561-642d8700-95fa-11eb-8d91-0bcff364c880.png" width="750;" />

3. From there you select your app type - Ruby in my case, and then you can get all you need, including the `newrelic.yml` file(the download button gives it), and then you place it in the `config/` folder of your app.

<img src="https://user-images.githubusercontent.com/17362519/113585651-858e7300-95fa-11eb-80cb-1c2142282b38.png" width="750;" />

4. Then restart your app and should be seeing stats for your app in a few minutes.  Here you see your app now:

<img src="https://user-images.githubusercontent.com/17362519/113585790-b373b780-95fa-11eb-9d40-fbffae29672f.png" width="750;" />

<img src="https://user-images.githubusercontent.com/17362519/113585707-9b9c3380-95fa-11eb-936f-013437ca7d12.png" width="750;" />


If you wanted to add another APM for another application you would hit the `+ Add more data` button in the upper right.

#### Useful Links

[https://docs.newrelic.com/docs/agents/ruby-agent/configuration/ruby-agent-configuration/](https://docs.newrelic.com/docs/agents/ruby-agent/configuration/ruby-agent-configuration/)

[https://docs.newrelic.com/docs/agents/ruby-agent/installation/install-new-relic-ruby-agent/](https://docs.newrelic.com/docs/agents/ruby-agent/installation/install-new-relic-ruby-agent/)

[https://discuss.newrelic.com/t/unable-to-go-to-settings-or-notice-a-place-to-download-the-newrelic-yml-file-in-nr-one/144166/2](https://discuss.newrelic.com/t/unable-to-go-to-settings-or-notice-a-place-to-download-the-newrelic-yml-file-in-nr-one/144166/2)

