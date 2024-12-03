# A3-Cypress-Test
describe('Demoblaze Functional Tests', () => {
  const baseUrl = 'https://www.demoblaze.com';

  // Teste 1: Login com credenciais válidas
  it('Should log in with valid credentials', () => {
    cy.visit(baseUrl);
    cy.get('#login2').click(); // Abre o modal de login
    cy.get('#loginusername').type('testuser'); // Insere o username
    cy.get('#loginpassword').type('testpassword'); // Insere a senha
    cy.get('button[onclick="logIn()"]').click(); // Clica no botão de login
    cy.contains('Welcome testuser').should('be.visible'); // Verifica se o login foi bem-sucedido
  });

  // Teste 2: Adicionar produto ao carrinho
  it('Should add a product to the cart', () => {
    cy.visit(baseUrl);
    cy.contains('Laptops').click(); // Clica na categoria de Laptops
    cy.contains('Sony vaio i5').click(); // Seleciona o produto
    cy.get('.btn-success').click(); // Adiciona ao carrinho
    cy.on('window:alert', (text) => {
      expect(text).to.contains('Product added'); // Verifica o alerta
    });
  });

  // Teste 3: Logout
  it('Should log out successfully', () => {
    cy.visit(baseUrl);
    cy.get('#login2').click(); // Abre o modal de login
    cy.get('#loginusername').type('testuser'); // Insere o username
    cy.get('#loginpassword').type('testpassword'); // Insere a senha
    cy.get('button[onclick="logIn()"]').click(); // Faz login
    cy.contains('Welcome testuser').should('be.visible'); // Confirma o login
    cy.get('#logout2').click(); // Faz logout
    cy.contains('Log in').should('be.visible'); // Confirma que o logout foi bem-sucedido
  });
});


module.exports = {
  e2e: {
    baseUrl: "https://www.demoblaze.com", // Define a URL base para os testes
    setupNodeEvents(on, config) {
      // Implementação de eventos do Node.js, se necessário
    },
  },
};
