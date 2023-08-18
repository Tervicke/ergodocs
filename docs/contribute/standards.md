# Ecosystem Standards

## V1 Identity 

 #       | Description                                                  | [NIST §](https://pages.nist.gov/800-63-3/sp800-63b.html) |
 ------- | ------------------------------------------------------------ | -------------------------------------------------------- |
 **1.1** | Ensure all associated account passwords are at least 12 characters long ([C6](https://owasp.org/www-project-proactive-controls/#div-numbering)) | 5.1.1.2                                                  |
 **1.2** | Ensure all accounts such as Telegram admins, GitHub, and any associated Email accounts use appropriate multi-factor authentication | 6.1.1                                                    |

## V2 Development

 #       | Description                                                  | [CWE](https://cwe.mitre.org/) |
 ------- | ------------------------------------------------------------ | ----------------------------- |
 **2.1** | Ensure server configuration is hardened according to the recommendations of the application server and frameworks in use | 16                            |
 **2.2** | Ensure all components are up to date, preferably using a dependency checker during build or compile time ([C2](https://owasp.org/www-project-proactive-controls/#div-numbering)) | 1026                          |
 **2.3** | Ensure no secrets are within source code, preferably using a secrets scanner in CI environments ([C8](https://owasp.org/www-project-proactive-controls/#div-numbering)) | 798                           |
 **2.4** | Ensure analytics for third-party providers are configured |                            |
 **2.5** | Ensure code is open-source and publicly audited by the community |                            |

### Recommendations

 #       | Description                                                  |
 ------- | ------------------------------------------------------------ |
 **2.2** | Use [Snyk](https://snyk.io/) or [DependencyCheck](https://github.com/jeremylong/DependencyCheck) |
 **2.3** | Use [Semgrep](https://github.com/marketplace/actions/semgrep-action) with [Secrets Policy](https://semgrep.dev/p/secrets) |
 **2.4** | Ensure [analytics](analytics.md) are connected on sites like defillama |

## V3 Community Administration

 #       | Description                                               |
 ------- | --------------------------------------------------------- |
 **3.1** | Ensure Telegram groups have anti-spam protection in place |
 **3.2** | Ensure Discord groups have anti-spam protection in place  |
 **3.3** | Work towards reducing friction between chats |
 **3.4** | Strive to boost engagement |
 **3.5** | Make efforts to educate your community |

### Recommendations

 #       | Description                                                  |
 ------- | ------------------------------------------------------------ |
 **3.1** | Enable [OrgRobot](https://tgdev.io/bot/orgrobot) with custom questions |
 **3.1** | Consider using [tgdev](https://tgdev.io/bot/orgrobot) which has a few handy free bots like [daysandbox_bot](https://tgdev.io/bot/daysandbox_bot) & [grep_robot](https://tgdev.io/bot/grep_robot) |
 **3.2** | The built-in spam protection should be sufficient if properly configured |
 **3.3** | Consider [bridging your chats](bridge.md) with the Ergo Discord |
 **3.3** | Get your Telegram added to [@ErgoChats](https://t.me/Ergo_Chats) on Telegram |
 **3.3** | Create a PR to add yourself to this documentation |
 **3.3** | Get added on [ergcube](https://ergcube.com/index.php?do=static&page=socials) and [sigmaverse](https://github.com/ergoplatform/sigmaverse) |
 **3.4** | Participate in the weekly developer and marketing updates |
 **3.4** | Participate in [ergoforum.org/c/marketing](https://www.ergoforum.org/c/marketing/13) |
 **3.5** | Teach good principles like [KYA](kya.md) |
 **3.5** | Warn users of scams being executed on the platform, particularly in response to support requests |
